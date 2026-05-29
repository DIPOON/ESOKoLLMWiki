# Log

Append-only record of ingests, queries, lint passes, and structural maintenance.

---

## [2026-06-01] setup | v2 reset 초기 vault 구조

- v1 wiki (1616 페이지, 989 raw processed)를 `archive/v1-claude-flat-wiki` 브랜치에 백업.
- `wiki/` 전체 삭제 + `raw/Lore/_ingested/` + `raw/Online/_ingested/` + `raw/Books/_ingested/` 모두 원위치 복원.
- 새 `wiki/` 구조 생성: people·places·concepts·factions·events·quests·texts·source-notes·decisions.
- 새 `CLAUDE.md` 작성 (ESO-first + layer separation + 영문 canonical + 분류 폴더 + source-note 시스템 + 1 source 1 commit).
- 새 `wiki/overview.md`, `wiki/index.md`, `wiki/log.md`, `wiki/decisions/2026-06-01-v2-reset.md` 작성.

## [2026-06-01] setup | Obsidian raw 제외 + processed 폴더 사전 생성

- `.obsidian/app.json`의 `userIgnoreFilters`를 `"raw/"` → `"^raw/"`로 정확화 (prefix match).
- `raw/processed/{Lore,Online,Books}/` 사전 생성 (CLAUDE.md §5 구조).
- commit `3feabf026`.

## [2026-06-01] setup | v2 polish (리뷰 의견 4건 반영)

- **High**: `raw/_manifest.md` v1 잔재 (`wiki/termbase/` + `_ingested/` 패턴 가리킴) 삭제. v1 정보는 archive 브랜치에 보존.
- **Medium**: `.gitignore`를 v2 패턴으로 갱신. 기존 `_ingested/` negate (`!raw/Books/_ingested/` 등) 제거. v2는 `raw/<ns>/*` ignore + `raw/processed/<ns>/`는 자동 추적 (negate 불필요).
- **Low**: `.idea/` git 추적 해제 (`git rm --cached -r .idea/`) + `.gitignore`에 `.idea/` 추가. 워킹 트리 파일은 유지 (사용자 IDE 개인 설정).
- **Medium**: `wiki/decisions/2026-06-01-v2-reset.md`의 ⏳ pending 항목들 ✅로 갱신 (Obsidian 설정·시작 source·pace·Codex 역할 모두 합의됨).

## [2026-06-01] setup | v2 polish 2 (리뷰 의견 7건 추가 반영)

CLAUDE.md 정정:

- **High** §6 Page Naming — entity page vs source-note 구분 명확화. "UESP·공식 출처와 일대일 대응"은 source-note에만 적용. entity는 *하나의 entity = 하나의 페이지*고 여러 source가 그 페이지에 합류.
- **Medium** §6 — source-note naming 다양화. `UESP - <Ns> - <Title>` 외에 `Official ESO - ...`, `ESO Book - ...`, `ESO Quest Dialogue - ...`, `Screenshot - ...`, `Dev Material - ...` 명시.
- **Medium** §11 Cascade 제한 — stub 생성 기준 강화. "substantive"의 구체적 정의: (1) source 핵심 행위자·장소·사건·진영이거나 (2) 현재 source에서 2개 이상 fact 추출 시에만. 평문 vs stub 판정 표 추가.
- **Low** §4 — raw/ 제외를 "권장"에서 "필수 (required)"로 격상.
- **Low** §17 — "첫 사용자 입력 받기 전에 자동으로" → "세션에서 편집·ingest 작업을 시작하기 전에"로 정정. 메모리 확인 단계 추가.
- **Low** §15.2 — log.md 정정 규칙 추가. *과거 수정 금지, superseding entry append* 원칙.
- **Medium** §9 Ingest Workflow — source_path는 처음부터 final processed 경로 작성. raw move는 commit 직전 step 9. step 10 verify (path 실제 존재 + 원본 제거 + 모두 stage) 추가. step 11이 commit.
- **Medium** §13 Lint Workflow — 2 스코프 분리. Full vault lint (모든 wiki/*)과 Content-page lint (encyclopedia content만). meta-page (index/log/overview/decisions) + source-note 별도 규칙. 풀 lint *자주* 권장.

---

## v1 마지막 상태 (참고)

`archive/v1-claude-flat-wiki` 브랜치 마지막 commit:

- 페이지 1616, raw processed 989, Orphan 0, Broken 687, 360 commit.
- 주요 한계: source-note 시스템 부재, 내적 ES 지식 stub 양산, 시대 혼합 claim, *asterisk 강조 남발, layer separation 미준수.
- 상세: [[decisions/2026-06-01-v2-reset]] 참조.
