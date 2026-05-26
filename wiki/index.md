# Wiki Index

CLAUDE.md §5.5에 따라 위키 전체 카탈로그. 매 batch 종료 시 갱신.

마지막 갱신: 2026-05-26 (seed-import #1)

---

## Termbase

총 **619 페이지**. 카테고리별 분포:

| 카테고리 | 수 | 비고 |
|---|---|---|
| [던전](termbase/) | 217 | 시드: 던전 시트 |
| [지명](termbase/) | 175 | 시드: 지명사전 |
| [기타](termbase/) | 66 | 시드: 기타사전 — 세부 재분류 필요 (게임용어/책/진영/종족 등) |
| [인물](termbase/) | 61 | 시드: 인명사전 |
| [아이템](termbase/) | 61 | 시드: 아이템 |
| [게임용어](termbase/) | 39 | 시드: 확정됨 + 확정됨2 |

> 옵시디언에서 `termbase/` 폴더 탐색 또는 `category: 인물` Dataview 쿼리로 카테고리별 보기.

## Decisions (시드 import)

이번 시드 자료에서 *결정 후보* / *정책 자료*는 termbase가 아닌 `decisions/` 에 단일 .md로 보존.

| 파일 | 행수 | 내용 |
|---|---|---|
| [[decisions/seed-debate]] | 339 | "토론중" 시트 — 미결정 후보 |
| [[decisions/seed-merkmire]] | 97 | "머크마이어(임시 통합)" 시트 |
| [[decisions/seed-policy]] | 33 | "번역자들 참고논의" — 음차/의역 정책 (style-guide 시드) |
| [[decisions/seed-npc-tone]] | 10 | "npc말투" — 캐릭터 톤 (style-guide 시드) |
| [[decisions/seed-pending]] | 4 | "보류" |
| [[decisions/seed-quest-naming]] | 4 | "퀘스트 관련" — 퀘스트 명명 정책 |
| [[decisions/seed-import]] | - | 시드 import 마찰점 종합 + CLAUDE.md 갱신 후보 |

## Style Guide

- `wiki/style-guide.md` — **미생성**. [[decisions/seed-policy]] + [[decisions/seed-npc-tone]]을 정리해서 만들 후속 작업.

## Lore

- `wiki/lore/` — **미생성**. 향후 번역 사이클에서 자연 생성.

## Sections

- `wiki/sections/` — **미생성**. DB 묶음 작업 시작 시 자연 생성.

---

## 다음 후속 작업 (우선순위 순)

1. **CLAUDE.md 갱신** — [[decisions/seed-import]]의 갱신 후보 4건 검토 후 §4b·§5·§5.1·§11 반영
2. **style-guide.md 초안** — seed-policy + seed-npc-tone 정수 추출
3. **멀티 항목 행 분리** — 글리프 등급/물약 접두어 25개 페이지 재생성
4. **중복 슬러그 정리** — 9개 동일 매핑 중복 통합
5. **기타사전 세부 분류** — 66개를 게임용어/책/진영 등으로
