# Wiki Index

CLAUDE.md §5.5에 따라 위키 전체 카탈로그. 매 batch 종료 시 갱신.

마지막 갱신: 2026-05-26 (seed-import #1 + A' 정리)

---

## Termbase

총 **626 페이지**. 카테고리별 분포:

| 카테고리 | 수 | 비고 |
|---|---|---|
| [던전](termbase/) | 211 | 시드: 던전 시트 (충돌 6건 통합) |
| [지명](termbase/) | 174 | 시드: 지명사전 (충돌 1건 통합) |
| [게임용어](termbase/) | 91 | 시드: 확정됨 39 + 기타사전 36 + 글리프 16 |
| [인물](termbase/) | 61 | 시드: 인명사전 |
| [아이템](termbase/) | 61 | 시드: 아이템 |
| [종족](termbase/) | 15 | 기타사전에서 재분류 (Ayleid/Chimer/Dremora 등 + 생물·데이드릭 종) |
| [진영](termbase/) | 9 | 기타사전에서 재분류 (Bloody Fist/Iron Wheel 등 단·조직) |
| [기타](termbase/) | 4 | 모호/메타 (adept, almsivi, nebarra, vicecanon) |

**채택 근거 상태**:
- **168 페이지**: 디씨 자료에 description이 있어 채택 근거 본문 풍부 (예: [[termbase/soul-gem]])
- **451 페이지**: 단순 매핑(영문→한글)만 있음. 채택 근거 본문은 `## TODO: 채택 근거 추가`. fix-as-you-go 정책(§4 step 1)에 따라 번역 사이클 중 자연 보강.

**플래그된 페이지**:
- `flags: [split-done]` — 1 페이지(글리프 등급 시리즈) 분리 완료 색인.
- `flags: [retired, superseded-by-아이템-시트]` — 1 페이지(물약 접두어 시리즈). 옵션 B 결정으로 retire. ([[decisions/seed-import]] 마찰점 #12)
- 슬래시 슬러그 — 3 페이지(`jerkin--robe`, `kinlady--kinload`, `kinlord--kinlady`). 정상 매핑이지만 후속 lint 대상.

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

- [[style-guide]] — ✅ 신설(2026-05-27, `feature/remains` #1). 10개 섹션:
  - §1 명명 형식 (퀘스트/인명/지명/아이템/재료/스킬)
  - §2 세트 아이템 명명 (접미/접두/유니크)
  - §3 NPC 말투 (카짓 3인칭 + 알려진 NPC 7명 톤 표)
  - §4 퀘스트 번역 룰
  - §5 가구 명칭 (미정)
  - §6 ⚠ **특수 문자·시스템 토큰 보존** (변수/색상/단복수/ID/명사속성)
  - §7 검수·맞춤법
  - §8 자주 헷갈리는 케이스
  - §9 가이드 갱신 정책
  - §10 출처

## Lore

- `wiki/lore/` — **미생성**. 향후 번역 사이클에서 자연 생성.

## Sections

- `wiki/sections/` — **미생성**. DB 묶음 작업 시작 시 자연 생성.

---

> *시간순 변경 이력은 [[log]] 참조.* index.md는 현재 상태 카탈로그만 유지.

## 미해결 후속 작업 (우선순위 순)

1. ~~style-guide.md 초안 작성~~ **✅ 완료 (feature/remains #1)**: 10 섹션, [[style-guide]] 참조. 후속은 *번역 사이클 중 발견되는 룰*을 §9 정책에 따라 갱신.
2. **451 TODO 마커 페이지 채택 근거 보강** — 새 후속 작업. 한 번에 다 못함. *번역 사이클 중 자연 발견 + 점진적 보강* 권장.
3. ~~멀티 항목 25 페이지 분리~~ **✅ 완료 (feature/remains #3 + 후속)**: 글리프 16 분리. 물약 9는 옵션 B 결정 — 아이템 시트 매핑이 정본, 시리즈 페이지는 retire 색인으로.
4. ~~충돌 접미사 9 파일 통합~~ **✅ 완료 (feature/remains #4)**
5. ~~기타사전 66건 세부 분류~~ **✅ 완료 (feature/remains #5)**: 60건 재분류(게임용어 36 / 종족 15 / 진영 9). 모호한 4건(adept, almsivi, nebarra, vicecanon)은 기타 유지. 분류는 Claude 수동 판단이라 사용자 검토 권장.
6. **decisions/seed-* 별도 폴더 분리 여부** — 다음 외부 시드 자료 ingest 한 번 더 보고 결정 (반복 신호 룰).
7. **슬래시 슬러그 정리** — 3 파일(`jerkin--robe`, `kinlady--kinload`, `kinlord--kinlady`)을 분리 또는 alias 통합. [[decisions/seed-import]] 마찰점 #11.
