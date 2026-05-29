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

---

## v1 마지막 상태 (참고)

`archive/v1-claude-flat-wiki` 브랜치 마지막 commit:

- 페이지 1616, raw processed 989, Orphan 0, Broken 687, 360 commit.
- 주요 한계: source-note 시스템 부재, 내적 ES 지식 stub 양산, 시대 혼합 claim, *asterisk 강조 남발, layer separation 미준수.
- 상세: [[decisions/2026-06-01-v2-reset]] 참조.
