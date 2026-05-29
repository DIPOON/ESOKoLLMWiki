# ESOKoLLMWiki — Claude 운영 지침 (v2)

이 보관함은 **Elder Scrolls Online (ESO) 한국어 lore 백과사전**이다. ESO 2E 582 시기를 *primary frame*으로 두고, 필요할 때만 broader TES context로 보강한다. Claude (agent)가 raw source를 *읽고·검증하고·정제하여* wiki 페이지로 file back한다.

## 목적

1. **ESO 한국어 reference**: 사용자가 ESO 게임 중·후에 lore 질문·인물·진영·역사 자문에 활용
2. **agent의 ESO lore 전문성 축적**: 매 ingest마다 source-backed 페이지가 늘어남
3. **(후순위) 번역 plugin**: 영문 canonical 페이지명·frontmatter aliases를 [ESOKo](https://github.com/DIPOON/ESOKo) Laravel이 *DB sync* 가능. 본 wiki는 *그것 없이도 자립*

**v1 → v2 reset 근거**: [[decisions/2026-06-01-v2-reset]]. v1은 `archive/v1-claude-flat-wiki` 브랜치 보존.

---

## 1. Agent Roles

- **Claude (primary maintainer)**: 본 위키의 *주된 ingest·페이지 작성·유지보수* 담당. 본 문서의 규칙을 따른다.
- **Codex (reviewer / advisor)**: 평소엔 *리뷰·자문·품질 게이트* 역할. diff·출처 coverage·layer 경계·commit granularity·lore 충실도 점검. 사용자가 명시 reassign하지 않는 한 broad autonomous ingest 금지.
- **사용자**: source curator + question + direction reviewer.

---

## 2. Scope (도메인 제약)

- **ESO-first, TES-aware**. 2E 582 frame이 default.
- 4E·3E·1E·Merethic의 fact를 *ESO 시기에 소급 적용 금지*. broader context로 분리.
- ESO 외 ES 게임은 *clarify할 때만* 인용. 그 출처도 명시.
- gameplay build guide가 아닌 *lore 백과사전*.
- 게임 system은 lore·setting·narrative·faction·place·in-world text와 관련될 때만 포함.

---

## 3. Source Hierarchy (출처 우선순위)

순서대로 우선:

1. **ESO in-game** — quest, dialogue, book, item text, environmental text, screenshot
2. **Official ESO** — 공식 페이지·트레일러·chapter description·patch note·dev material
3. **Other ES games in-game** — 다른 ES 시리즈의 *in-game* material
4. **Community reference** (UESP 등) — navigation·cross-check 용. *primary 인용 아님*
5. **Fan interpretation** — forum·video·interview·out-of-game text. *반드시* lower-confidence·external 마크업

**Never invent citations.** 출처 backing 없는 claim은 *unsourced·tentative*로 명시하거나 *생략*.

---

## 4. Layer Separation (절대 원칙)

`raw/` vs `wiki/` 경계는 **절대 흐려지면 안 된다**.

- `raw/` = **immutable source archive**. 내용 수정 금지. 처리 후 `raw/processed/`로 이동.
- `wiki/` = **검증된 백과사전**. 모든 페이지는 source-backed.
- **wiki 본문 `[[X]]`는 *반드시* `wiki/.../X.md`에 페이지가 존재**해야 함. 미해결 링크는 *stub 즉시 생성* 또는 *평문화* 둘 중 하나.
- **raw 노드로 직접 wikilink 금지**. raw 안의 UESP MediaWiki 마크업 (`{{Lore Link|X}}`, `[[Lore:X|...]]`)이 Obsidian vault scope에서 해석되어 graph 오염되는 것 *방지 필요*.
- **Obsidian vault scope에서 raw/ 제외**: `.obsidian/app.json`의 `userIgnoreFilters`에 `^raw/` 추가 권장. graph·검색·링크 해석에서 raw 노드 분리.
- **source 인용**은 다음 셋 중 하나:
  - **source-note 링크**: `[[UESP - Lore - X]]` (wiki/source-notes/ 안)
  - **frontmatter `source_path:`** (raw 경로 명시)
  - **Sources 섹션의 평문 경로** (마지막 fallback)
- **단순 언급**은 평문. 한 페이지에서 한 번 스쳐가는 entity는 stub 만들지 말고 평문.

---

## 5. 레포 구조

```
ESOKoLLMWiki/
├── CLAUDE.md                  ← 본 문서
├── raw/                       ← immutable source archive (Obsidian vault scope에서 제외)
│   ├── Lore/                  ← UESP Lore: 처리 대기
│   ├── Online/                ← UESP Online: 처리 대기
│   ├── Books/                 ← 책 dump: 처리 대기
│   ├── processed/             ← 처리 완료 source (source namespace 보존)
│   │   ├── Lore/
│   │   ├── Online/
│   │   └── Books/
│   └── ESO (고유)명사 번역 통일안.xlsx
└── wiki/                      ← 검증된 백과사전
    ├── people/                ← 인물
    ├── places/                ← 장소
    ├── concepts/              ← 신학·마법·시스템·우주론 개념
    ├── factions/              ← 진영·집단·길드
    ├── events/                ← 역사적 사건
    ├── quests/                ← ESO quest (lore 의미가 있을 때만)
    ├── texts/                 ← in-world 책·시·편지·일기
    ├── source-notes/          ← 1 source = 1 note
    ├── decisions/             ← 메타-결정 (YYYY-MM-DD-topic.md)
    ├── index.md               ← 컨텐츠 카탈로그
    ├── log.md                 ← 시간순 append-only
    └── overview.md            ← 위키 high-level 맵
```

---

## 6. Page Naming

- **영문 canonical**: 파일명·wikilink 모두 영문. UESP·공식 출처와 일대일 대응.
  - 예: `Molag Bal.md`, `The Planemeld.md`, `Psijic Order.md`, `36 Lessons of Vivec, Sermon 29.md`
- **본문은 한국어**. 한국어 lore 백과사전이 본질.
- **frontmatter `aliases:`에 한글·별칭** 등록. Obsidian 한국어 검색은 alias로 hit.
- *singular canonical* 우선 (`Dark Anchor.md` 보다 `Dark Anchors.md`가 UESP 정통이면 그쪽).

---

## 7. Standard Frontmatter

페이지에 의미 있는 필드만 사용 (다 채울 필요 없음):

```yaml
---
type: person | place | faction | event | concept | text | quest | source-note
name: <영문 canonical>
aliases: [한글, 영문 별칭, ...]
era: Second Era | First Era | Merethic | ... (해당 시)
appears_in: [The Elder Scrolls Online, ...]
related: [[Other Page]], ...
status: stub | partial | developed
source_priority: eso-first
last_updated: YYYY-MM-DD
---
```

**source-note 전용 필드**:

```yaml
type: source-note
name: UESP - Lore - X
source_type: community-reference | official-eso | in-game-book | ...
source_path: raw/processed/Lore/X.md
ingested: YYYY-MM-DD
related: [[Affected Entity 1]], ...
status: ingested
source_priority: community-crosscheck | eso-primary | ...
```

---

## 8. Standard Page Sections

페이지 type에 맞춰 *적응*. 모든 섹션을 다 강요하지 않음. stub은 짧아도 됨.

```markdown
# <Page Name>

## Summary
<2-4문장 한국어 요약>

## ESO Context
<2E 582 frame 안에서의 의미. 가장 중요한 섹션>

## Broader TES Context
<후대 era 또는 other ES games 정보. 명시적으로 분리>

## Chronology
<시간순 정리 — event·quest 페이지에서 특히 유용>

## Related People / Places / Factions
<wikilink로 cross-ref>

## Interpretive Issues
<source 모순·불확실성·논쟁 — 매우 중요. 솔직히 명시>

## Sources
- [[UESP - Lore - X]]
- [[UESP - Online - Y]]
- raw/processed/Lore/X.md (직접 참조 시)
```

---

## 9. Ingest Workflow (1 source 단위)

**1 source = 1 ingest = 1 commit**. 배치 commit 금지.

1. **Read source** from `raw/`.
2. **Create source-note** under `wiki/source-notes/UESP - <Namespace> - <Title>.md`. Summary + Key Claims Extracted + Source Limits + Follow-Up Sources.
3. **Identify affected entities** (people·places·factions·events·concepts·texts·quests).
4. **Create missing pages as stubs** — but **only for entities the source explicitly names with substantive content**. 단순 언급은 stub 만들지 말고 평문.
5. **Update existing pages conservatively** — uncertainty 보존, source 경계 명시. claim마다 어느 source에서 왔는지 본문에서 추적 가능하게.
6. **Add Obsidian links** — wiki/ 내부만. raw 노드 링크 금지.
7. **Update `wiki/index.md`** — 새 페이지·material change 반영.
8. **Append `wiki/log.md`** — 한 줄: `## [YYYY-MM-DD] ingest | <source> | <touched pages summary>`.
9. **Move raw to `raw/processed/<namespace>/`** — source namespace (Lore/Online/Books) 보존.
10. **Single commit** — `Ingest UESP <Namespace>:<Title>` 같은 명확한 메시지.

**Redirect 처리**: raw 파일이 다른 raw의 redirect면 같은 ingest 배치에서 함께 처리·이동.

---

## 10. Commit Workflow

- **1 source = 1 commit** 원칙. tight하게 묶인 source bundle (redirect 등)만 예외.
- 무관한 raw 파일을 *덤으로 stage 금지*.
- 한 commit 안에는 *해당 source가 야기한* wiki 페이지·source-note·index·log·processed-move *모두 포함*.
- broad catch-up commit 금지 (provenance 가림).
- `report.md` 같은 *operational report*는 commit 하지 않음 (사용자 요청 시만).
- commit 메시지: `Ingest UESP Lore:Planemeld`, `Lint after Five Companions ingests`, `Decision: v2 reset` 같이 *명확*.

---

## 11. Cascade 제한

v1에서 가장 큰 실수가 *내적 ES 지식만으로 빈 stub 양산*이었다. v2에서는:

- **stub 생성 조건**: 처리 중인 raw source가 해당 entity를 *substantive하게* 언급 (단순 이름 1회 ≠ substantive)
- **내적 지식 동원 금지**: ES 일반 지식으로 "당연히 알 만한" 페이지를 *raw 검증 없이* 생성 금지
- **Orphan 0은 *결과*가 아니라 *부산물***: 페이지 생성 → 그 페이지를 인용하는 wiki 페이지가 자연히 생기는 게 정상. 반대로 "orphan이라서 억지로 link 추가" 금지
- **단순 언급은 평문**: "*Vivec City의 Temple Canton*" 이 한 번 스쳐가면 stub 만들지 말고 평문 유지

---

## 12. Query Workflow

사용자 lore 질문 응대:

1. **`wiki/index.md` 먼저** 확인
2. **관련 wiki 페이지 읽기** (raw 직행 금지)
3. **raw는 wiki가 불충분할 때 또는 사용자가 source-level 검증 요청 시에만**
4. 답변에서 **ESO fact / Broader TES context / interpretation 명확히 구분**
5. 답이 *persistent knowledge로 가치 있으면* wiki/에 file back 제안

---

## 13. Lint Workflow

정기 점검 (각 N source 또는 사용자 요청):

- **무출처 페이지** (Sources 섹션 비어있는 wiki/)
- **시대 혼합 claim** (ESO 시기 페이지에 4E·3E 정보가 mark 없이 섞임)
- **중복·일관성 없는 페이지명** (`Volkihar`·`Volkihar Clan`·`Volkihar Vampires` 등)
- **inbound·outbound 링크 누락**
- **중요 mentioned entity가 페이지 없음**
- **source 간 모순** (Interpretive Issues에 명시했는지)
- **stale source-note 또는 index entry**
- **raw 노드 직접 wikilink** (있으면 즉시 제거)

각 lint pass는 `wiki/log.md`에 기록.

---

## 14. Claude가 *하지 않는 것*

- ❌ **raw 파일 내용 수정**. 이동만 OK.
- ❌ **사용자 모호한 발언을 정책으로 해석**. "좋아요" / "그런 생각도 있어요"는 결정이 아님. 결정점에서는 AskUserQuestion 또는 명확 확인.
- ❌ **카테고리 사전 채움** — "16 Daedric Princes 다" 같은 batch 생성. seed import는 별도 결정 + decisions/ 절차.
- ❌ **broken link 방치** — `[[X]]` 박았으면 *그 시점에* X stub 생성 또는 평문화. *나중에 채울게* 금지.
- ❌ **내적 지식 동원 stub** — raw에 명시 없는 entity는 페이지 생성 금지.
- ❌ **raw 노드 직접 wikilink** — source 인용은 source-note 또는 frontmatter source_path.
- ❌ **synthesis 페이지 회피** — 사용자 질문이 valuable 합성을 만들면 wiki에 file back.
- ❌ **`*` asterisk 강조 남발** — v1에서 본문 가독성 해친 패턴. `**bold**`·`*italic*` markdown 표준만 사용.

---

## 15. index + log + overview

### 15.1 index.md
- **컨텐츠 카탈로그** + 페이지별 one-line summary
- 새 페이지·material change마다 갱신
- 형식: `- [[<Page Name>]] — <one-line summary>`

### 15.2 log.md
- **append-only**. 매 ingest·query·lint·decision *한 줄 이상*.
- 형식: `## [YYYY-MM-DD] <kind> | <descriptor> | <metric>`

### 15.3 overview.md
- **위키 high-level 맵**. 현재 focus·source queue·축이 되는 page cluster.
- 가끔 갱신 (source queue가 바뀌거나 focus shift할 때).

---

## 16. 번역 plugin (후순위, Phase 2)

본 wiki는 *번역 도구의 부속이 아니다*. 그러나 *기존 ESOKo Laravel 프로젝트*와 연동할 plugin layer가 *미래에* 추가될 수 있다:

- frontmatter `aliases: [한글]`을 Laravel이 DB sync
- 영문 canonical 페이지명이 *Laravel terms 테이블의 primary key 후보*
- frontmatter `target_de`, `target_ja` 등 다국어 슬롯이 *미래에 추가 가능*

Phase 2 진입 시점은 불명. 본 문서는 *그것 없이도 자립*하도록 설계.

---

## 17. 세션 시작 의례

Claude는 첫 사용자 입력 받기 *전에* 자동으로:

1. `wiki/log.md` 마지막 5줄 → "어제까지 X 작업"
2. **Lint 빠른 카운트**: wiki/ 페이지 수, raw/ 처리 vs 미처리, broken·orphan 카운트
3. `git status` (working tree 점검)

세션 종료 시: `wiki/log.md`에 세션 요약 한 줄 + 정리 commit 권유.

---

## 18. 점진적 개선

본 문서는 *살아있는 명세*. 운영 중 발견되는 새 정책·예외·실수:

- 한두 줄 보완 → 본 문서 직접 추가
- 큰 정책 변경 → `wiki/decisions/<YYYY-MM-DD>-<topic>.md` 결정 기록 + 본 문서 갱신
- 분기당 한 번 `wiki/log.md` lint — 정책 변경이 일관 반영됐는지 확인
