---
type: misc
last_updated: 2026-06-01
---

# Overview

ESOKoLLMWiki v2 — ESO-first, TES-aware 한국어 lore 백과사전.

## 현재 상태

- 마이그레이션 직후 (v1 reset). 모든 페이지 새로 ingest 예정.
- v1 wiki (1616 페이지)는 `archive/v1-claude-flat-wiki` 브랜치에 보존.
- v1 reset 근거: [[decisions/2026-06-01-v2-reset]].

## 핵심 원칙

- **ESO 2E 582 frame이 default**. 후대 era는 Broader TES Context로 분리.
- **Layer separation**: raw/와 wiki/ 경계 엄수. wiki 본문 [[X]]는 wiki/.../X.md 보장.
- **Source-backed only**: 내적 ES 지식만으로 stub 양산 금지. 모든 substantive claim은 raw source backing.
- **1 source = 1 commit**: 배치 commit 금지, provenance 명확화.

## 폴더 구조

- `wiki/people/` — 인물
- `wiki/places/` — 장소
- `wiki/concepts/` — 신학·마법·시스템·우주론 개념
- `wiki/factions/` — 진영·집단·길드
- `wiki/events/` — 역사적 사건
- `wiki/quests/` — ESO quest (lore 의미가 있을 때만)
- `wiki/texts/` — in-world 책·시·편지·일기
- `wiki/source-notes/` — 1 source = 1 source-note
- `wiki/decisions/` — 메타-결정 (YYYY-MM-DD-topic.md)

## 시작 영역 후보 (논의 중)

다음 ingest 사이클의 시작점:

- ESO main quest + Planemeld 축 (Codex 위키 시작점과 동일)
- Vvardenfell·Summerset·Coldharbour 한 zone storyline
- Three Banners War + 3 alliance 정치
- Tribunal Temple + Morrowind 신학

구체적 시작점은 사용자와 합의 후 결정.

## Source Queue 정책

- 1 source 단위 ingest + 1 commit.
- 처리된 raw는 `raw/processed/<namespace>/`로 이동 (Lore/Online/Books namespace 보존).
- raw/는 Obsidian vault scope에서 제외 (graph·검색 분리).
