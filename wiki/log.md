# Log

Append-only record of ingests, queries, lint passes, and structural maintenance.

---

## [2026-06-01] setup | v2 reset 초기 vault 구조

- v1 wiki (1616 페이지, 989 raw processed)를 `archive/v1-claude-flat-wiki` 브랜치에 백업.
- `wiki/` 전체 삭제 + `raw/Lore/_ingested/` + `raw/Online/_ingested/` + `raw/Books/_ingested/` 모두 원위치 복원.
- 새 `wiki/` 구조 생성: people·places·concepts·factions·events·quests·texts·source-notes·decisions.
- 새 `CLAUDE.md` 작성 (ESO-first + layer separation + 영문 canonical + 분류 폴더 + source-note 시스템 + 1 source 1 commit).
- 새 `wiki/overview.md`, `wiki/index.md`, `wiki/log.md`, `wiki/decisions/2026-06-01-v2-reset.md` 작성.
- 아직 source ingest 시작 전. 다음 단계: 시작 source 합의 + Obsidian vault scope 분리 (raw/ 제외) 설정.

---

## v1 마지막 상태 (참고)

`archive/v1-claude-flat-wiki` 브랜치 마지막 commit:

- 페이지 1616, raw processed 989, Orphan 0, Broken 687, 360 commit.
- 주요 한계: source-note 시스템 부재, 내적 ES 지식 stub 양산, 시대 혼합 claim, *asterisk 강조 남발, layer separation 미준수.
- 상세: [[decisions/2026-06-01-v2-reset]] 참조.
