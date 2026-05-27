# Wiki Index

CLAUDE.md §5.5에 따라 위키 전체 카탈로그. 매 batch 종료 시 갱신.

마지막 갱신: 2026-05-26 (seed-import #1 + A' 정리)

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

**채택 근거 상태**:
- **168 페이지**: 디씨 자료에 description이 있어 채택 근거 본문 풍부 (예: [[termbase/soul-gem]])
- **451 페이지**: 단순 매핑(영문→한글)만 있음. 채택 근거 본문은 `## TODO: 채택 근거 추가`. 후속 lint에서 디씨/UESP/일본판 참조하여 보강 대상.

**플래그된 페이지**:
- `flags: [needs-split, multi-item-cell]` — 2 페이지. 한 셀에 여러 단어가 줄바꿈으로 들어간 케이스(글리프 등급/물약 접두어). 향후 16+9 = 25 페이지로 분리.
- 충돌 접미사 페이지 (`*--시트-행.md` 형태) — 9 페이지. 모두 동일 매핑 중복이라 *둘째 파일 삭제 lint* 대상.

> 옵시디언 Dataview로 `flags`, `status`, `category`별 동적 조회 가능.

## Decisions (시드 import 결과물)

이번 시드 자료의 *원본 추출물*은 `decisions/seed-*.md`에 보존. (§5.4 정의의 *결정 한 줄 로그*와 형식이 다름 — 다음 시드 자료 import 시 별도 폴더 분리 여부 결정 예정.)

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

> *시간순 변경 이력은 [[log]] 참조.* index.md는 현재 상태 카탈로그만 유지.

## 미해결 후속 작업 (우선순위 순)

1. **style-guide.md 초안 작성** — `seed-policy` + `seed-npc-tone`에서 정수 추출. 번역 품질에 가장 큰 영향. *가장 가치 있는 후속*.
2. **451 TODO 마커 페이지 채택 근거 보강** — 새 후속 작업. 한 번에 다 못함. *번역 사이클 중 자연 발견 + 점진적 보강* 권장.
3. **멀티 항목 25 페이지 분리** — `flags: needs-split` 표시된 2 파일을 16+9 개별 페이지로 재생성.
4. ~~충돌 접미사 9 파일 통합~~ **✅ 완료 (feature/remains #4)**
5. **기타사전 66건 세부 분류** — 게임용어/책/진영/종족 등으로.
6. **decisions/seed-* 별도 폴더 분리 여부** — 다음 외부 시드 자료 ingest 한 번 더 보고 결정 (반복 신호 룰).
7. **슬래시 슬러그 정리** — 3 파일(`jerkin--robe`, `kinlady--kinload`, `kinlord--kinlady`)을 분리 또는 alias 통합. [[decisions/seed-import]] 마찰점 #11.
