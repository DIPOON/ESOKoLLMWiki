# ESOKoLLMWiki — Claude 운영 지침

이 보관함은 **Elder Scrolls Online 지식 wiki**다. [Andrej Karpathy의 LLM Wiki 패턴](https://gist.github.com/karpathy)을 ES 도메인에 구현한 것. Claude (agent)가 raw source를 *흡수·합성·정제*하여 *ES 전문가가 되도록 *증분적으로 *지식 그래프*를 *구축·유지*한다.

목적:
1. **agent의 *ES 전문성 *축적*** — 매 ingest마다 wiki가 더 풍부해짐
2. **사용자의 *ES 반려 AI*** — lore 질문, NPC·진영·역사 자문, 게임 시 길동무
3. **(후순위) 번역 API plugin** — frontmatter `term:` 필드를 [ESOKo](https://github.com/DIPOON/ESOKo) Laravel이 *DB sync*. 본 wiki는 *그것 없이도 자립*

미션 변경 근거: [[decisions/2026-05-28-mission-pivot]].

---

## 1. 레포 구조

```
ESOKoLLMWiki/
├── CLAUDE.md                    ← 본 문서 (스키마)
├── raw/                         ← immutable 원본 자료
│   ├── Lore/                    ← UESP Lore: 처리 대기 + _ingested/
│   ├── Online/                  ← UESP Online: 처리 대기 + _ingested/
│   ├── Books/                   ← 책 dump: 처리 대기 + _ingested/
│   └── ESO (고유)명사 번역 통일안.xlsx
└── wiki/                        ← Claude 소유 — flat namespace
    ├── *.md                     ← 모든 entity·book·synthesis 페이지 (한 폴더)
    ├── decisions/               ← 메타-결정 (별도 분리, append-only)
    │   └── YYYY-MM-DD-<topic>.md
    ├── index.md                 ← 카탈로그 (one-line summary, 카테고리별)
    ├── log.md                   ← 시간순 append-only
    └── style-guide.md           ← 번역 plugin용 톤·규칙 (Phase 2)
```

원칙:
- **raw/는 *immutable*** — 파일 *내용 수정 금지*. 처리 후 *_ingested/로 이동*만 OK.
- **wiki/는 *flat***. lore/, termbase/ 같은 *namespace 분기 없음*. *모두 wiki/<slug>.md*.
- **wiki/decisions/만 분리** — 메타-결정 문서는 *entity·book과 본질이 *다름*. 시간 prefix.

---

## 2. 페이지 종류 — frontmatter `kind:`

모든 wiki 페이지는 frontmatter 첫 줄에 `kind:` 명시. 4종:

| kind | 정의 | 예 |
|---|---|---|
| **`entity`** | 재사용 가능 노드: 인물·장소·신성·종족·진영·유물·사건·개념 | vivec, daedric-princes, three-banners-war, adamantine-tower |
| **`book`** | raw에서 흡수한 *단일 책/문서*. 시리즈는 *권 페이지 + 색인 페이지* | 36-lessons-of-vivec-sermon-29, 2920-시리즈-색인 |
| **`synthesis`** | 여러 source 통합 *분석·comparison·합성*. *raw 1:1 요약이 *아님* | tribunal-신앙-변천, daedric-princes-16-비교 |
| **`misc`** | index, log, style-guide 등 메타 (decisions/는 별도 폴더라 kind 불필요) | index, log, style-guide |

frontmatter 표준 필드 (kind 별):

```yaml
---
name: 표시 이름 (한글 우선)
aliases: [영문, 한글, 별칭...]
kind: entity | book | synthesis | misc
category: 인물 | 지명 | 신성 | 진영 | 종족 | 사건 | 게임용어 | 유물 | 책 | ...
# kind=book의 경우:
series: <시리즈명>
series_index: <권 번호>
author: <저자>
source_uesp: raw/<폴더>/_ingested/<file>.md
# kind=entity의 경우 (번역 plugin용 — 후순위):
term: <영문 원어>
target_ko: <한국 통용 표기>
ingested_at: YYYY-MM-DD
---
```

---

## 3. 워크플로 (카파시 정신)

### 3.1 Ingest — raw → wiki

한 source 처리 1 사이클:

1. **Source 전체 read** (첫 문단만 X — 모든 섹션)
2. **사용자와 *takeaway 논의*** (Claude 핵심 짧게 보고, 사용자가 강조/제외 결정). *자동화 금지 — 매 source 1회 *대화 필수*. 사용자가 명시적으로 *"여러 개 자동 진행"* 요청 시에만 예외.
3. **wiki 페이지 1+ 생성/갱신**:
   - kind=book 페이지 신설 (raw → 요약 + 핵심)
   - **본문에 [[entity-slug]] 링크 박을 때, 그 entity 페이지가 *없으면 *즉시 *최소 stub* 생성** (broken link 금지). stub = frontmatter + 한두 문장.
4. **언급된 *기존 entity 페이지 *cascading 갱신*** — 이 source가 *그 entity에 *새 정보 *추가*하면 *해당 페이지에 *문단·섹션 *추가*. 카파시: *한 source → 10-15 페이지 touch*.
5. **wiki/log.md** 한 줄 append: `## [YYYY-MM-DD HH:MM] ingest | <source> | touched: N pages`
6. **raw/<source>.md → raw/<폴더>/_ingested/**.

### 3.2 Query — wiki → 사용자

1. *index.md 먼저 *읽고 *관련 페이지 찾기*
2. *해당 페이지 + cross-ref 따라가며 *합성*
3. 답변 — markdown · 표 · comparison · 그래프 등
4. **답이 *valuable한 *합성*이면 *wiki/<topic>.md (kind=synthesis)로 *filed back***. 채팅에 휘발 금지.

### 3.3 Lint — 정기 health check

매 사이클 끝 (또는 50 commit마다)에 확인:

- **Broken link**: `[[X]]` 박혔는데 `wiki/X.md`도 없는 경우. *즉시 stub 생성 또는 *redirect*.
- **Orphan**: 다른 페이지에서 *in-link 0인 wiki 페이지*. *시리즈 색인에 흡수 + 가치 없으면 *삭제 검토*.
- **Missing concept**: source에서 *반복 등장하는데 *전용 페이지 없는 entity*. *우선순위 추가*.
- **Missing cross-ref**: A가 B를 인용하는데 B에 *A 역참조 없음* (양방향 끊김).
- **Stale claim**: 새 source가 *기존 페이지의 *주장과 *모순*. *모순 명시 + decisions/로 기록*.
- **Data gap**: 사용자 *질문에 *못 답하는 영역* — *어떤 source 더 필요한지 *제안*.

---

## 4. 페이지 규약

### 4.1 슬러그
- *kebab-case + 한글 가능*. 영문 entity는 *소문자 + 어포스트로피·괄호 제거 + 공백 → '-'*.
- 책 시리즈 권 페이지는 *번호 prefix 유지* (예: `36-lessons-of-vivec-sermon-29.md`, `2920-morning-star-v1.md`, `1-스라시안-역병.md`).
- 한글 표기가 *커뮤니티 통용 (예: 셰오고라스·아말렉시아)*이면 *frontmatter `aliases:`에 *영문 병기*. 슬러그는 *영문 (`sheogorath.md`) 또는 *한글 (`셰오고라스.md`) 어느 쪽이든 *기존 패턴 따름*.

### 4.2 위키링크
- `[[<slug>]]` 또는 `[[<slug>|<표시>]]` — **prefix 없음**. `[[lore/X]]`, `[[termbase/X]]` *전부 금지* (마이그레이션 후 자동 교체됨).
- 한 페이지 안에서 같은 entity 재인용 시 *display 일관* 유지.
- *broken 즉시 생성*: 링크 박을 때 *대상 페이지 없으면 *그 시점에 *stub*.

### 4.3 카테고리 (`category:`)
*closed list*:
- `인물` — 역사적 인물 + NPC (Vivec, Abnur Tharn, Mannimarco)
- `지명` — 도시·지역·차원 (Tamriel, Coldharbour, Vivec City)
- `신성` — Aedra·Daedra·기타 신 (Sheogorath, Akatosh, Hist)
- `진영` — 길드·가문·조직 (Thieves Guild, House Telvanni, Aldmeri Dominion)
- `종족` — 종족 (Altmer, Khajiit, Vampire, Werewolf)
- `사건` — 역사 사건 (Battle of Red Mountain, Soulburst, Red Year)
- `유물` — 무기·아티팩트 (Chrysamere, Amulet of Kings, Wrathstone)
- `개념` — 게임용어·신학 개념 (CHIM, Walking Ways, Dragon Break)
- `책` — kind=book 페이지 *모두* (시·편지·일기·우화 등 *세부 분류 폐기*)
- `synthesis` — kind=synthesis 페이지

이 외 자유 추가 *금지*. 새 카테고리 필요 시 *decisions/에 기록 후 *본 문서 갱신*.

### 4.4 frontmatter `related:`
선택적. 양방향 cross-ref *명시 도구*. 예: `related: [vivec, almalexia, sotha-sil]`.

---

## 5. 번역 plugin (후순위, Phase 2)

본 wiki는 *번역 도구의 *부속이 아니다*. 그러나 *기존 ESOKo Laravel 프로젝트*와 연동할 수 있는 *plugin layer*가 *미래에* 추가될 수 있다:

- frontmatter `term:` + `target_ko:` 필드를 *Laravel이 *읽어 *MySQL `terms` 테이블 *sync*
- frontmatter `target_de`, `target_ja` 등 *다국어 슬롯* — *disambiguation 근거*
- 번역 묶음 워크플로 (`claude_batches` 테이블, `/api/claude/*` 엔드포인트, `EnumUser::CLAUDE`) — *모두 *미구현 + 후순위*

Phase 2 진입 시점은 *불명*. 본 문서는 *그것 없이도 *완전 자립*하도록 설계.

---

## 6. 세션 시작 의례

Claude는 첫 사용자 입력 받기 *전에* 자동으로:

1. `wiki/log.md` 마지막 5줄 → "어제까지 X 작업"
2. **Lint 빠른 카운트**: broken link 수, orphan 수, raw 진행도. (사용자가 *그것 보고 우선순위 줄 수 있게*)
3. `git status` (변경 안 된 파일 있는지)

세션 종료 시: `wiki/log.md`에 세션 요약 한 줄 + `git add + commit` 권유.

---

## 7. Claude가 *하지 않는 것*

- ❌ **raw 파일 *내용 수정***. *이동·분류만 OK* (예: `raw/Lore/X.md` → `raw/Lore/_ingested/X.md`).
- ❌ **사용자의 *모호한 발언을 *정책으로 해석***. *"좋은 것 같아요" / "그런 생각 있어요" 같은 *의견* 발언은 *결정이 아님*. AskUserQuestion 또는 직접 확인 거쳐 진행.
- ❌ **카테고리 사전 채움** — 자연 trigger 없이 *"Daedric Princes 16 전체" 같은 *카테고리 *batch 생성*. 그건 *seed import (사용자 정책 결정 + decisions/seed-policy-<자료>.md) 절차*.
- ❌ **broken link 방치** — `[[X]]` 박았으면 *X 페이지 *그 시점에 *최소 stub 또는 *redirect*. *나중에 채울게* 금지.
- ❌ **raw → wiki *1:1 flat 변환 production line*** — *한 source = *최소 *entity 1 + book 1 = 2 page touch* + *기존 entity cascading 갱신*. *책 요약만 박고 *링크 빈 노드 *남발 금지*.
- ❌ **synthesis 페이지 회피** — *사용자 질문이 *valuable 합성을 만들면 *wiki에 *filed back*. 채팅에 휘발 금지.
- ❌ **claude_score 자동 채점** (현재 범위 밖).

---

## 8. index + log

### 8.1 index.md
- *카탈로그* + *카테고리별 페이지 *one-line summary 포함*. 매 ingest 끝 갱신.
- 형식: `- [[<slug>|<표시>]] — <one-line summary>`.
- 동적 조회는 옵시디언 Dataview 활용 가능 (frontmatter 기반).

### 8.2 log.md
- *append-only*. 매 ingest·query·lint·decision *한 줄*.
- 형식: `## [YYYY-MM-DD HH:MM] <kind> | <descriptor> | <metric>`
- 예: `## [2026-05-28 14:00] ingest | A Game at Dinner | touched: 1 book + 3 entity stub`

---

## 9. 점진적 개선

본 문서는 *살아있는 명세*. 운영 중 발견되는 새 정책·예외·실수는:
- 한두 줄짜리 보완 → 본 문서 직접 추가
- 큰 정책 변경 → `decisions/<YYYY-MM-DD>-<topic>.md`에 결정 기록 + 본 문서 갱신
- 분기당 한 번 `wiki/log.md` lint — *정책 변경이 *일관 반영됐는지 확인*
