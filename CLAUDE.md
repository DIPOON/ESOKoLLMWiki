# ESOKoLLMWiki — Claude 운영 지침

이 보관함은 [ESOKo](https://github.com/DIPOON/ESOKo) (esokr.org) 프로젝트의 **큐레이션 레이어**다. ESOKo가 번역 작업물을 MySQL에 저장하는 *작업 산출물 저장소*라면, 이 위키는 *어떻게 번역할지를 결정하는 뇌*다. 두 레포는 같은 MySQL DB를 공유하지만 코드는 독립이다.

Claude는 이 보관함에서 작업할 때 본 문서의 규약을 따른다.

---

## 0. 두 레이어 — 위키 ↔ ESOKo

```
┌────────────────────────────────────────────────────────────┐
│ ESOKoLLMWiki (이 레포, 옥시디안 보관함)                       │
│ 역할: 큐레이션. 번역 결정의 근거·맥락·기억.                    │
│ 사람 도구: 옵시디언. Claude가 만지는 곳: wiki/                │
└────────────────────────────────────────────────────────────┘
                            ↑
                            │ 같은 MySQL DB 공유
                            ↓
┌────────────────────────────────────────────────────────────┐
│ ESOKo (별도 레포, esokr.org 운영 서비스)                      │
│ 역할: 작업물 저장. lang_id_unknown_index_offsets, terms 등.   │
│ Claude는 DB 직접 접근 금지. 반드시 Laravel API 경유.          │
└────────────────────────────────────────────────────────────┘
```

**원칙**: Claude는 위키 파일은 직접 read/write. 그러나 DB는 *절대 직접 update/insert 하지 않는다*. 반드시 ESOKo Laravel의 `/api/claude/*` 엔드포인트를 통한다. 이유: `translation_logs` 인서트, Elasticsearch 인덱싱, 캐시 무효화 등 부수효과가 Controller에 묶여 있다. 직접 DB 치면 부수효과 누락 → 운영 무결성이 깨진다.

---

## 📍 현재 단계 (Phase Marker)

> **Phase 1 — 합의 단계 (현재).** 본 문서는 *명세*다. 다음은 *아직 구현 전*:
> - ESOKo `/api/claude/*` 엔드포인트 (§2.2): **미구현**
> - `claude_batches`, `lang_official_translations` 테이블 (§2.3): **미마이그레이션**
> - `EnumUser::CLAUDE = 6`: **미정의**
>
> **그래서:**
> - ✅ **실행 가능**: §4-b (시드 import — 위키 파일만 만짐), `wiki/` 페이지 read/write, ESOKo 레포 파일 *읽기*만 (예: `app/Enum/EnumPatch.php`).
> - ❌ **실행 불가**: §4 (번역 묶음 워크플로), §6 의례 중 *ESOKo API* 의존 항목, §7 응급 롤백.
> - **§4 워크플로 시도 시 첫 호출에서 404로 정지하는 게 정상.** ESOKo 측 PR이 들어와 위 미구현 항목이 채워진 뒤 *Phase 2*.
>
> 이 마커는 Phase 2 진입(API+테이블 마이그레이션 완료) 시 갱신·삭제한다.

---

## 1. 레포 구조

```
ESOKoLLMWiki/
├── CLAUDE.md                    ← 본 문서
├── raw/                         ← 원본 자료 (immutable, 사람이 채움)
│   └── LLM Wiki.md, …
├── wiki/                        ← Claude가 만들고 관리 (큐레이션 산출물)
│   ├── index.md                 ← 카탈로그
│   ├── log.md                   ← 작업 로그 (append-only)
│   ├── style-guide.md           ← 톤·존댓말·섹션별 정책
│   ├── termbase/                ← 용어 결정 (DB terms와 1:1 연결)
│   │   └── <slug>.md
│   ├── lore/                    ← NPC·지역·진영·책 (번역 컨텍스트)
│   │   └── <한글이름>.md
│   ├── sections/                ← (lang_id, unknown) 섹션별 메타
│   │   └── <lang_id>-<unknown>.md
│   └── decisions/               ← 번역 결정 로그
│       └── YYYY-MM-DD.md
└── tools/                       ← (옵션) 자주 쓰는 SQL/스크립트
```

---

## 2. ESOKo Laravel API (Claude 전용) — 명세

Claude가 호출할 엔드포인트. **구현은 ESOKo 레포 측 작업이다.** 본 문서는 *명세 (계약)* 다.

### 2.1 인증
- Laravel Sanctum 발급 API 토큰. `Authorization: Bearer <token>` 헤더.
- 토큰은 환경변수 `ESOKO_CLAUDE_TOKEN`. 위키 보관함에 평문 저장 금지.
- 베이스 URL: `ESOKO_API_BASE` (예: `http://localhost:8000`).

### 2.2 엔드포인트

```
GET /api/claude/batch
  query: lang_id, unknown, index_from, index_to
  response: {
    items: [
      {
        lang_id, unknown, index, offset,
        en_text, current_text, state, user_id,
        official_translations: {de: "...", fr: "...", ja: "...", ...}
      }, …
    ],
    terms_in_scope: [          // 묶음의 영문 텍스트에서 발견된 termbase 항목
      {term, target_text, note}
    ],
    neighbors: {               // 묶음 직전·직후 ±3 행 (컨텍스트)
      before: [...], after: [...]
    }
  }

POST /api/claude/batch/start
  body: {context: "사람용 묘사", lang_id, unknown, index_from, index_to, note}
  response: {batch_id}
  → claude_batches 에 row 생성. 모든 묶음 작업의 첫 호출.

POST /api/claude/translate
  body: {
    batch_id,
    items: [{lang_id, unknown, index, offset, text}, …]
  }
  response: {updated: N}
  → 메인 테이블 + translation_logs + Elasticsearch 일관 처리.
  → 자동으로 user_id = EnumUser::CLAUDE(6), state = EnumState::ML(30).

POST /api/claude/batch/complete
  body: {batch_id, state, summary}
  → claude_batches.state 갱신.

POST /api/claude/term-suggest
  body: {term, target_text, note, source_batch_id}
  → terms 테이블에 후보로 인서트 또는 term_logs에 검토 대기 항목.

GET /api/claude/term?term=…
  → terms 테이블 단건 조회.
```

### 2.3 신설 필요 DB 테이블

```sql
-- Claude 작업 묶음 메타
CREATE TABLE claude_batches (
  id BIGINT PRIMARY KEY AUTO_INCREMENT,
  context TEXT,                   -- "Auridon Vestige dialog 124-12"
  lang_id INT,
  unknown SMALLINT,
  index_from MEDIUMINT,
  index_to MEDIUMINT,
  item_count INT,
  state TINYINT,                  -- IN_PROGRESS=10, COMPLETE=20, REVIEWED=30, ROLLED_BACK=40
                                  -- (EnumState와 별도 enum. EnumBatchState 신설 권장)
  note TEXT,                      -- 위키 어느 페이지를 컨텍스트로 썼는지 등
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  INDEX (lang_id, unknown, index_from, index_to)
);
-- 정본: ESOKo `database/migrations/*_create_claude_batches.php` (Phase 2 진입 시).
-- 본 SQL은 합의 시점 스냅샷이므로 마이그레이션 후 어긋날 수 있음. 충돌 시 ESOKo migration이 정본.

-- ZOS 공식 다국어 원문 (disambiguation 참조용)
CREATE TABLE lang_official_translations (
  id BIGINT PRIMARY KEY AUTO_INCREMENT,
  lang_id INT,
  unknown SMALLINT,
  `index` MEDIUMINT,
  language_code VARCHAR(8),       -- 'de', 'fr', 'es', 'ja', …
  text TEXT,
  patch_version SMALLINT,
  UNIQUE KEY (lang_id, unknown, `index`, language_code, patch_version),
  INDEX (lang_id, unknown, `index`)
);
```

`EnumUser::CLAUDE = 6` 추가 (ZENIMAX=1 … GOOGLE_TRANSLATOR=5 다음).

---

## 3. 컨텍스트 묶음 단위

**기본 단위: `(lang_id, unknown)` 안의 ±N 인접 인덱스.**

- N은 세션마다 사용자가 지정. 일반적으로 10~50.
- 같은 묶음은 *같은 화자·같은 톤·같은 narrative context* 일 확률이 높다 — 이게 termbase·style-guide·lore의 가치를 살리는 단위.
- 참조: `ESOKo::TranslationController::getSub`이 사람 화면에 ±3 인접을 보여주는 것과 같은 사상.

**예외**: 책(book) 본문은 한 책 전체가 한 묶음. UI 라벨은 같은 unknown 안에서 더 넓은 범위 가능.

---

## 4. 번역 워크플로 (한 묶음 한 사이클)

사용자로부터 "X 묶음 번역해줘"를 받으면 다음 순서를 따른다.

1. **컨텍스트 로드 (위키 측)**
   - `wiki/sections/<lang_id>-<unknown>.md` — 없으면 샘플 5행으로 추정 후 신설.
   - `wiki/style-guide.md` — 전체.
   - 묶음에 등장하는 고유명사에 대해 `wiki/termbase/<slug>.md` 읽기.
     - **fix-as-you-go**: 해당 페이지의 "## 채택 근거"가 `## TODO: 채택 근거 추가` 마커이면, 본 묶음 처리 중에 description을 작성하여 동시에 보강한다. 외부 lint 사이클 없이 자기 정리.
   - 등장 엔터티에 대해 `wiki/lore/<이름>.md` 읽기 (있으면).

2. **묶음 시작 (DB 측)**
   - `POST /api/claude/batch/start` → `batch_id` 받기.

3. **묶음 데이터 받기**
   - `GET /api/claude/batch?lang_id=…&unknown=…&index_from=…&index_to=…`
   - 응답의 `official_translations`가 있으면 *반드시* 참고 (§8).

4. **번역**
   - 위키 컨텍스트 + 다국어 참조로 한국어 산출.
   - 신규 고유명사 발견 시 *후보로만* 마킹. 이 단계에서 termbase 정식 등록 금지.

5. **DB 제출**
   - `POST /api/claude/translate` (50~200행 단위로 끊어서).

6. **위키 환류**
   - 신규 termbase 후보 → `wiki/decisions/YYYY-MM-DD.md`에 append.
   - 신규/갱신 lore 페이지 → `wiki/lore/<이름>.md` 작성/수정.
   - `wiki/log.md`에 한 줄: `## [YYYY-MM-DD HH:MM] batch=N | lang_id=X unknown=Y ix=A-B | <묘사>`

7. **묶음 종료**
   - `POST /api/claude/batch/complete`.

8. **사용자 보고**
   - 처리 행 수, 신규 용어 후보 N개, 신규 lore 페이지 N개, 모호한/위험한 항목 요약.

---

## 4-b. 시드 import 워크플로 (외부 자료 → 위키)

§4가 *DB 번역 묶음 1개*를 다룬다면, 4-b는 *외부 시드 자료 (xlsx/csv/txt 등)*를 위키로 흡수하는 별도 워크플로다. 발동 조건:
- DB가 아닌 외부 파일에서 *기존 결정들*을 흡수하는 경우.
- 한 묶음이 아닌 *대량 데이터* (수십~수천 행).
- 사용자가 *해당 자료를 표준으로 따른다*고 정책 결정한 경우.

### 4-b.1 순서

1. **자료 schema 파악**
   - 시트/탭/섹션별 구조 분석. 컬럼 의미 식별 (term / target / note / category 등).
   - **사람 검토 1회**: 처음 2-3행을 사용자에게 보여주고 컬럼 매핑 확인.

2. **시트별 Tiered 처리 결정** (CLAUDE.md §5 구조에 매핑)
   - 명확한 termbase 후보 (확정/인명/지명/아이템/던전 등) → `wiki/termbase/<slug>.md` 자동 생성.
   - 정책/메타 (음차 규칙·NPC 톤·퀘스트 명명 등) → `wiki/decisions/seed-*.md` 또는 `wiki/style-guide.md` 통합 후보.
   - 미결정/보류 (토론중·보류·임시 등) → `wiki/decisions/seed-pending.md` 등 별도 보존. 정식 termbase로는 가지 않음.

3. **자동 import 실행**
   - 슬러그 정책(§5.0) + frontmatter 형식(§5.1) 적용.
   - 충돌·잘림·schema 불일치는 *검토 표시*만 남기고 진행 (중단하지 않음 — 단 *영문 같지만 한글 다른* 진짜 충돌은 중단).

4. **마찰점 종합 + CLAUDE.md 갱신 후보 기록**
   - `wiki/decisions/seed-import.md` (또는 회차별 `seed-import-N.md`)에 발견한 마찰점을 모두 기록.
   - 같은 종류 마찰이 2회 이상 누적되면 본 문서 갱신.

5. **사용자 보고**
   - 생성 페이지 수, 시트별 분포, 마찰점 N건, 후속 작업 후보.

6. **`wiki/log.md` 한 줄 append**
   ```
   ## [YYYY-MM-DD] seed-import #N | <자료명> | termbase N, decisions N, 마찰점 M
   ```

### 4-b.2 §4와의 차이점

| | §4 (번역 묶음) | §4-b (시드 import) |
|---|---|---|
| 입력 | DB의 `(lang_id, unknown)` 행들 | `raw/` 의 외부 파일 |
| 단위 | ±N 인접 인덱스 | 시트/카테고리 |
| API 호출 | claude_batches + translate + Elasticsearch | 없음 (위키 파일만) |
| 신규 term 처리 | 후보 마킹 → 사용자 채택 → API 등록 | **일괄 자동 등록** (사용자가 정책 선언 시) |
| 결과물 | DB UPDATE + decisions/ 한 줄 | termbase 다수 + decisions/seed-*.md |

---

## 5. 위키 페이지 규약

페이지 제목과 위키링크는 *한글 우선*, frontmatter `aliases`에 영문 병기. termbase 페이지는 영문 슬러그 (DB terms.term이 영문이라 1:1 매핑이 깔끔).

### 5.0 슬러그 생성 규칙 (termbase)

ESOKo `App\Http\Controllers\TermController::normalizeTerm`과 일관되게:

```
1. 소문자화 + trim
2. 앞 관사 (a/an/the) 제거 — 정규식 ^(a|an|the)\s+
3. 어포스트로피(') 제거
4. 공백을 '-'로 치환
5. [a-z0-9가-힣\-_] 외 문자 제거
6. 최대 60자. 초과 시 어절 경계('-')에서 잘림 + frontmatter `flags`에 검토 표시.
```

**충돌 처리**:
- *영문 같지만 한글 다른* 진짜 충돌 → 자동 import 중단, 사용자 결정 요청.
- *완전 동일 매핑 중복* (예: 대소문자만 다른 `Vestige` vs `vestige`) → 첫 등재본 유지, 둘째는 skip (또는 임시 `--<시트>-<행>` 접미사 + 후속 lint에서 통합).

### 5.1 termbase/&lt;slug&gt;.md

DB `terms` 테이블과 1:1 매핑. **DB가 정본** (target_text, note), **위키가 풍부판** (근거·후보·lore 링크).

```markdown
---
term: Auridon
target_ko: 아우리돈
target_de:                    # 미래 다국어 슬롯. suffix는 §2.2 official_translations.language_code (ISO 639-1)와 일치.
target_ja:                    # 예: de=독일어, ja=일본어, fr=프랑스어, es=스페인어, zh=중국어
aliases: [Auridon, 아우리돈]
category: 지명                # 인물 / 지명 / 진영 / 종족 / 책 / 게임용어 / 던전 / 아이템 / 기타
status: 확정                  # 확정 / 토론중 / 보류 / 제안
first_seen_batch: 12          # 시드 import에서 온 경우 비워둠
source_sheet:                 # (시드 import 한정) 출처 시트명
source_row:                   # (시드 import 한정) 출처 행번호
source_file:                  # (시드 import 한정) 출처 파일 경로
related: [[알드메리-자치령]], [[엘프]]
---

# Auridon (아우리돈)

## 채택 근거
- 디씨 ESO 커뮤니티 표준 '아우리돈' 따름.
- '어리돈'은 영어 발음에 더 가까우나 한국 ESO 커뮤니티 정착 표기 우선.

## 다른 후보
- 어리돈 — 영어 발음 기반. 채택 안 함.
- 오리돈 — 일본어판 オーリドン 기반. 채택 안 함.

## 관련 lore
- [[알드메리-자치령]]의 본거지 섬.
- 1막 메인 퀘스트의 주요 무대.
```

### 5.2 lore/&lt;이름&gt;.md

```markdown
---
name: 아우리돈
aliases: [Auridon]
category: 지역
factions: [[알드메리-자치령]]
first_seen_batch: 12
---

# 아우리돈

## 개요
서머셋 군도의 동쪽 섬. 알드메리 자치령의 정치적 중심지.

## 번역 시 주의
- 화자가 알트머일 경우 격식 높임말 기본.
- 신성한 장소(예: 더 베스타지) 언급은 의고체.

## 등장 NPC
- [[라이엘레-푸레닐]] — 의회 의원

## 출처
- batch_id=12 (2026-05-25)
- UESP: https://en.uesp.net/wiki/Online:Auridon
```

### 5.3 sections/&lt;lang_id&gt;-&lt;unknown&gt;.md

```markdown
---
lang_id: 124
unknown: 12
estimated_type: 다이얼로그        # UI / 다이얼로그 / 책본문 / 스킬설명 / 아이템설명 / 기타
sample_indices: [100, 101, 105, 110, 200]
---

# 124-12

## 추정
NPC 다이얼로그 (샘플 5행 모두 1·2인칭 대화체).

## 톤 가이드
- 화자에 따라 존댓말/반말 결정. 인접 ±3 내 톤 일관성.
- 1행 끝의 화자 정보가 다음 행에 이어지는 패턴 있음.
```

### 5.4 decisions/YYYY-MM-DD.md

날짜별 append-only.

```markdown
# 2026-05-25

## [10:30] batch=12, term 채택: Auridon → 아우리돈
근거: 디씨 표준. [[termbase/auridon]] 생성.

## [11:00] batch=14, 톤 정책: 셰오고라스 대사는 광기체
근거: 캐릭터 성격상 격식체 부자연스러움. [[style-guide]] 갱신.
```

### 5.5 index.md

카테고리별 카탈로그. 매 batch 종료 시 갱신.

### 5.6 log.md

append-only. 모든 batch·decision·lint·시드 import를 *한 줄 요약 + 선택적 sub-bullet ≤5개*로 기록.

- 일상 번역 batch·decision은 단일 한 줄로 충분.
- 시드 import 같은 큰 작업은 한 줄 요약 + ≤5 sub-bullet (산출물 수/마찰점 수 등).

---

## 6. 세션 시작 의례

Claude는 사용자의 *첫 입력을 받기 전에* 자동으로 다음을 수행하고 한 줄씩 보고한다.

1. `wiki/log.md` 마지막 5줄 → "어제 X 묶음 작업"
2. `git status` (옥시디안 보관함) → "커밋 안 된 변경 N개"
3. ESOKo `EnumPatch::CURRENT_VERSION` → "현재 ESO 패치 버전 V"

세션 종료 시: `wiki/log.md`에 세션 요약 한 줄 append, `git add + commit` 사용자에게 권유.

---

## 7. kr.lang 패치 반영 정책 — A안 (현재 정책 유지)

- `CreateKrLang.php`는 `lang_id_unknown_index_offsets` 전체를 패치에 반영. state 필터 없음.
- Claude 번역도 *바로* 다음 패치 빌드에 들어간다.
- 익명 사람 번역(`UNKNOWN=40`)과 동일 신뢰 등급.

**보완:**
- `EnumUser::CLAUDE = 6`. user_id로 Claude 번역 구별 가능 → 통계, 응급 롤백, 검토 우선순위.
- 운영 시작 직후 처음 10~20 묶음은 사용자가 sampling 검토.

**응급 롤백 (예시):**

> ⚠ **이 SQL은 사람이 직접 실행한다. Claude 자동 실행 금지** (§11과 충돌). Claude는 batch 식별자 조회·SQL 본문 *제시*만 가능, `mysql` 명령 실제 실행은 본인 손으로. Phase 2 진입 후 `/api/claude/batch/rollback` 엔드포인트가 생기면 그 경로로 흡수.

```sql
UPDATE lang_id_unknown_index_offsets
SET text = '', user_id = 1 /*ZENIMAX*/, state = 10 /*RAW*/
WHERE lang_id = ? AND unknown = ? AND `index` BETWEEN ? AND ?;
-- 위 4개 인자는 claude_batches에서 조회
```

---

## 8. 다국어 참조 (Disambiguation)

**ZOS 공식 다국어판은 disambiguation 단서.**

- 영어 "Fire!"만 보면 동사/명령 모호. 일본어 "撃て!" vs "火事だ!"로 갈림.
- `lang_official_translations` 테이블에 (de, fr, es, ja 등) 저장.
- `/api/claude/batch` 응답에 `official_translations` 슬롯 포함.

**원칙: 영어와 다른 언어가 충돌하면 *다국어 다수결* 우선.**
- 영어 1표 vs 독·불·일 3표 → 다국어 의미 채택.
- 영어판이 유일하게 다른 경우는 ZOS의 영문 누락/오기일 가능성이 높음 (다국어 번역자가 의미를 보고 옮긴 것).
- 모호한 케이스는 decisions/에 근거 기록 후 채택.

---

## 9. DB ↔ 위키 동기화 규칙

| 변경 위치 | 동기화 방향 | 트리거 |
|---|---|---|
| /glossary UI에서 term 추가/수정 | DB → 위키 | (수동/hook) Claude가 `wiki/termbase/` 생성·갱신 |
| Claude가 새 term 후보 발견 | 위키 → DB | `POST /api/claude/term-suggest` |
| 위키에서 target_text 수정 | 위키 → DB | Claude가 `POST /api/claude/term-suggest` (덮어쓰기) |
| 사람이 번역 화면에서 submit | DB만 | 위키 영향 없음 |
| Claude 번역 submit | DB만 (위키엔 decisions/만) | `POST /api/claude/translate` |

**원칙**: `target_text`/`note`는 DB가 정본, *근거 텍스트와 lore 링크*는 위키가 정본. 충돌 시 *DB의 사실값* + *위키의 맥락*을 양쪽 다 보존.

---

## 10. 보안·Attribution

- Claude 번역은 `user_id = EnumUser::CLAUDE(6)`. esokr.org UI는 사람 번역과 동일 처리 (번역자 기본 비공개, 사고 시만 한정 공개).
- API 토큰은 환경변수만. 위키 파일에 평문 금지.
- 본인 검토용 SQL은 `tools/queries/` 폴더. 비밀번호·접속 정보 평문 금지.

---

## 11. Claude가 하지 않는 것

- ❌ MySQL DB 직접 update/insert (반드시 API 경유).
- ❌ ESOKo 레포 코드 수정 (별도 작업).
- ❌ `raw/` 폴더 파일 수정 (immutable).
- ❌ 사용자 확인 없이 termbase 정식 등록 (decisions/에 후보로만, 사용자 채택 후 `/api/claude/term-suggest`).
  - **단서 — 시드 import 예외**: 사용자가 정책으로 일괄 채택을 선언한 시드 자료는 자동 일괄 등록 OK (§4-b 참조).
  - **권한 트리거 형식** (필수): 시드 일괄 등록은 *다음 두 조건 모두 충족 시에만* 진행한다.
    1. `wiki/decisions/seed-policy-<자료명>.md` 파일에 정책 결정이 명시적으로 기록되어 있음 (어떤 자료를 어떤 방식으로 일괄 채택하는지).
    2. 사용자가 해당 세션에서 *명시적*으로 진행을 승인 (예: "이 시드 자료 import 진행" 같은 직접 지시).
    
    채팅의 모호한 발언("이거 좋은 것 같아", "한 번 따라가자" 등)을 *정책 결정으로 해석 금지*. 의심스러우면 AskUserQuestion으로 명시 확인 후 진행.
- ❌ esokr.org 사용자에게 노출되는 번역문을 위키에 *대량 복제* 저장 (라이선스 경계).
- ❌ claude_score 자동 채점 (현재 버전 범위 밖. 컬럼은 `-1` 유지).

---

## 12. 점진적 개선

본 문서는 *살아있는 명세*다. 운영 중 발견되는 새 정책·예외·실수는:
- 한두 줄짜리 보완: 본 문서에 직접 추가.
- 큰 정책 변경: `decisions/`에 결정 기록 + 본 문서 갱신.

분기당 한 번 `wiki/log.md`를 훑어 정책 변경이 일관되게 반영됐는지 lint.
