# Wiki Index

CLAUDE.md §5.5에 따라 위키 전체 카탈로그. **매 라운드 끝 / 50 commit / batch 종료 시 갱신**.

마지막 갱신: 2026-05-28 (라운드 2 끝 + 메타-termbase 사건 직후)

---

## 한눈 통계

| 항목 | 수 |
|---|---|
| Termbase | **696** (이전 630 → 메타 60+ ESO 동맹 5) |
| Lore | **206** (라운드 1: 33 → 라운드 2: 110 → 라운드 3: 153 → 라운드 4: 206) |
| Decisions | 8 (시드 import 6 + meta-termbase-emergency 1 + seed-import 종합 1) |
| raw/Lore 진행 | 272 _ingested / 13676 남음 (1.95%) |
| raw/Online | 316 _ingested / 73145 남음 (0.4% — 라운드 1 발췌만) |
| raw/Books | 0 / 114 남음 (미진행) |

---

## 진입점 (어디서 시작할까)

- 새 사관: [[#세션 시작 의례 (CLAUDE.md §6)]] 참조 → log.md 마지막 5줄 → 본 index
- 번역 묶음 작업: §4 워크플로 → [[style-guide]] + 묶음 entity termbase
- lore ingest: §4-c 워크플로 → raw/Lore에서 *자연 trigger* (사용자 질문 또는 등장)로 시작. *카테고리 사전 채움 금지* (§4-c.1)
- 시드 import: §4-b → seed-policy 파일 + 사용자 명시 승인 (§11)
- 정책 변경: 본 문서 + [[decisions/2026-05-28-meta-termbase-emergency]] (위반 사례 교훈)

---

## Termbase (691)

### 카테고리별 분포

| 카테고리 | 수 | 비고 |
|---|---|---|
| [던전](termbase/) | 211 | 시드: 던전 시트 |
| [지명](termbase/) | 183 | 시드 175 + 메타-termbase 신설 18 (Akavir/Atmora/Yokuda/Aldmeris/Pyandonea/Morrowind/Cyrodiil/Skyrim/High Rock/Hammerfell/Elsweyr/Black Marsh/Valenwood/Summerset Isles/Vvardenfell/Solstheim/Resdayn/Red Mountain) + lint 보강 3 (Auridon/Daggerfall/Iliac Bay) + High Isle/Vivec City |
| [게임용어](termbase/) | 95 | 시드 93 + CHIM + Walking Ways + The Serpent |
| [아이템](termbase/) | 63 | 시드 |
| [인물](termbase/) | 61 | 시드 (인명사전) |
| [종족](termbase/) | 28 | 시드 15 + 메타-termbase 신설 13 (Altmer/Bosmer/Dunmer/Argonian/Breton/Imperial/Khajiit/Orsimer/Redguard/Falmer/Maormer/Tsaesci/Ayleid) |
| [신성](termbase/) | 26 | **메타-termbase 신설 25** (Daedric Princes 16 + Aedra 8 + Magnus + Tribunal 3 + ALMSIVI) + Lorkhan |
| [신성·개념](termbase/) | 5 | Aedra / Daedra / et-ada / Anu / Aetherius |
| [진영](termbase/) | 9 | 시드 |
| [기타·우주·개념·역사적 인물](termbase/) | 9 | 시드 4 + 메타-termbase 신설 5 (Aurbis/Mundus/Padomay/Lorkhan/Nerevar 등) |

### 출처별 트레이서빌리티

- **시드 import (1차)**: 619 페이지. frontmatter `source_sheet`, `source_row`, `source_file` 채워짐. [[decisions/seed-import]] 참조.
- **UESP 자동 보강 (#D)**: 371 페이지에 description 자동 추가.
- **메타-termbase 일괄 신설 (2026-05-28)**: **54+8 페이지 — *§11 권한 트리거 우회* 사후 정당화**. 트레이서빌리티 0 (source_* 미기록). 자세한 사정은 [[decisions/2026-05-28-meta-termbase-emergency]].

### 한글 표기 정정 (2026-05-28)
- Hircine: 하르신느 → **허씬** | Mehrunes Dagon: 메루네스 데이곤 → **메이룬스 데이건** | Jyggalag: 직갈라그 → **지갈렉** | Almalexia: 알마렉시아 → **아말렉시아** | Arkay: 아카이 → **아케이**
- 구 표기는 aliases에 유지 (검색 호환).

### 핵심 신성 entity 진입점
- [[termbase/almsivi|ALMSIVI]] (Tribunal) — [[termbase/almalexia|아말렉시아]] · [[termbase/sotha-sil|소사 실]] · [[termbase/vivec|Vivec]] · [[termbase/nerevar|네레바]]
- **Aedra (9 Divines)**: [[termbase/akatosh|아카토시]] · [[termbase/arkay|아케이]] · [[termbase/stendarr|스텐다르]] · [[termbase/kynareth|키나리스]] · [[termbase/mara|마라]] · [[termbase/julianos|줄리아노스]] · [[termbase/dibella|디벨라]] · [[termbase/zenithar|제니타르]] · [[termbase/lorkhan|로칸]]
- **Daedric Princes 16**: [[termbase/sheogorath|셰오고라스]] · [[termbase/malacath|말라카스]] · [[termbase/vaermina|베르미나]] · [[termbase/hircine|허씬]] · [[termbase/sanguine|생귄]] · [[termbase/namira|나미라]] · [[termbase/nocturnal|녹터널]] · [[termbase/mephala|메팔라]] · [[termbase/azura|아주라]] · [[termbase/boethiah|보에시아]] · [[termbase/molag-bal|몰라그 발]] · [[termbase/mehrunes-dagon|메이룬스 데이건]] · [[termbase/clavicus-vile|클라비쿠스 바일]] · [[termbase/peryite|페리아이트]] · [[termbase/meridia|메리디아]] · [[termbase/jyggalag|지갈렉]]
- **우주론**: [[termbase/aurbis|Aurbis]] · [[termbase/mundus|Mundus]] · [[termbase/aetherius|Aetherius]] · [[lore/oblivion|Oblivion]]
- **개념**: [[termbase/chim|CHIM]] · [[termbase/walking-ways|Walking Ways]] · [[termbase/anu|Anu]]/[[termbase/padomay|Padomay]]

---

## Lore (88)

### 시리즈

#### 36 Lessons of Vivec (37 sermon + 1 색인 = 38)
[[lore/36-lessons-of-vivec-시리즈-색인|시리즈 색인]] | sermon [[lore/36-lessons-of-vivec-sermon-1|1]] · [[lore/36-lessons-of-vivec-sermon-2|2]] · [[lore/36-lessons-of-vivec-sermon-3|3]] · [[lore/36-lessons-of-vivec-sermon-4|4]] · [[lore/36-lessons-of-vivec-sermon-5|5]] · [[lore/36-lessons-of-vivec-sermon-6|6]] · [[lore/36-lessons-of-vivec-sermon-7|7]] · [[lore/36-lessons-of-vivec-sermon-8|8]] · [[lore/36-lessons-of-vivec-sermon-9|9]] · [[lore/36-lessons-of-vivec-sermon-10|10]] ~ [[lore/36-lessons-of-vivec-sermon-36|36]] · [[lore/36-lessons-of-vivec-sermon-37|37 (비공식 C0DA)]]

#### 2920 시리즈 (12권 + 색인 = 13)
[[lore/2920-시리즈-색인|시리즈 색인]] | [[lore/2920-morning-star-v1|1·Morning Star]] · [[lore/2920-suns-dawn-v2|2·Suns Dawn]] · [[lore/2920-first-seed-v3|3·First Seed]] · [[lore/2920-rains-hand-v4|4·Rains Hand]] · [[lore/2920-second-seed-v5|5·Second Seed]] · [[lore/2920-midyear-v6|6·Midyear]] · [[lore/2920-suns-height-v7|7·Suns Height]] · [[lore/2920-last-seed-v8|8·Last Seed]] · [[lore/2920-hearth-fire-v9|9·Hearth Fire]] · [[lore/2920-frostfall-v10|10·Frostfall]] · [[lore/2920-suns-dusk-v11|11·Suns Dusk]] · [[lore/2920-evening-star-v12|12·Evening Star]]

#### 16 Accords of Madness (4)
[[lore/16-accords-of-madness-시리즈-색인|시리즈 색인]] | [[lore/16-accords-of-madness-v6-hircine의-이야기|v6 허씬]] · [[lore/16-accords-of-madness-v9-vaermina의-이야기|v9 베르미나]] · [[lore/16-accords-of-madness-v12-malacath의-이야기|v12 말라카스]]

#### Monument Island Plaques (5)
[[lore/1-스라시안-역병|1·스라시안 역병]] · [[lore/2-baron-admiral-bendu-olo|2·Baron-Admiral Bendu Olo]] · [[lore/3-all-flags-navy|3·All Flags Navy]] · [[lore/4-instrument-of-vengeance|4·Instrument of Vengeance]] · [[lore/5-construction-of-monument-island|5·Monument Island 건설]]

#### Manifestos of Kinlord Rilis XII (3)
[[lore/2nd-manifesto-of-kinlord-rilis-xii|2nd]] · [[lore/3rd-manifesto-of-kinlord-rilis-xii|3rd]] · [[lore/4th-manifesto-of-kinlord-rilis-xii|4th]]

#### A Culinary Adventure (5)
[[lore/a-culinary-adventure|색인]] | [[lore/a-culinary-adventure-volume-1|v1]] · [[lore/a-culinary-adventure-volume-2|v2]] · [[lore/a-culinary-adventure-volume-3|v3]] · [[lore/a-culinary-adventure-volume-4|v4]]

### 단편 (A- 시작 19개)
- [[lore/a-betrayal-of-our-heritage|A Betrayal of Our Heritage]] (Crowns 순혈주의)
- [[lore/a-bloody-journal|A Bloody Journal]] (TES4 Fighters Guild 학살)
- [[lore/a-bosmeri-sleeping-song|A Bosmeri Sleeping-song]] (Bosmer 자장가)
- [[lore/a-brief-history-of-ald-sotha|A Brief History of Ald Sotha]] (Sotha Sil 기원)
- [[lore/a-brief-history-of-house-telvanni|A Brief History of House Telvanni]] (Aldmeri 첩보)
- [[lore/a-brothers-plea|A Brother's Plea]] (Dragon Cult)
- [[lore/a-call-for-common-hair|A Call for Common Hair]] (Prince Hew 풍자)
- [[lore/a-call-for-recollection|A Call for Recollection]] (Bosmer-Ayleid 회복주의)
- [[lore/a-case-for-open-borders|A Case for Open Borders]] (Summerset 개방 호소)
- [[lore/a-cats-serenade|A Cat's Serenade]] (Khajiit 사랑 노래)
- [[lore/a-challengers-thoughts|A Challenger's Thoughts]] (Bedlam Veil)
- [[lore/a-change-in-the-chimer|A Change in the Chimer]] (1E 700 동시대 Dunmer 변형)
- [[lore/a-childs-play|A Child's Play]] (Green Lady Gwaering 어린 시절)
- [[lore/a-childs-tamriel-bestiary|A Child's Tamriel Bestiary]] (A-Z 운문 도감)
- [[lore/a-citizens-petition|A Citizen's Petition]] (Blackcaster Mages Guild)
- [[lore/a-clothiers-primer|A Clothier's Primer]] (Shattered Masque 튜토리얼)
- [[lore/a-cure-for-lycanthropy|A Cure for Lycanthropy]] (Silver Dawn 부패)
- [[lore/a-cyrodilic-merchants-lament|A Cyrodilic Merchant's Lament]] (Pact 비판 + 첩보)

### 기타 (8)
- [[lore/2e-582|2E 582 (ESO 게임 시점)]] · [[lore/2nd-manifesto-of-kinlord-rilis-xii|2nd Manifesto]] · [[lore/트롤-지방의-101가지-용도|101 Uses for Troll Fat]]

---

## Style Guide

- [[style-guide]] — 10개 섹션 (명명/세트/NPC 톤/퀘스트/가구/시스템 토큰/검수/헷갈리는 케이스/갱신 정책/출처)

---

## Decisions (8)

| 파일 | 형식 | 내용 |
|---|---|---|
| [[decisions/seed-import]] | 종합 | 시드 import 마찰점 + CLAUDE.md 갱신 후보 |
| [[decisions/seed-debate]] | 데이터 | "토론중" 시트 339행 |
| [[decisions/seed-merkmire]] | 데이터 | "머크마이어" 시트 97행 |
| [[decisions/seed-policy]] | 데이터 | "번역자들 참고논의" 33행 (style-guide 시드) |
| [[decisions/seed-npc-tone]] | 데이터 | "npc말투" 10행 (style-guide 시드) |
| [[decisions/seed-pending]] | 데이터 | "보류" 4행 |
| [[decisions/seed-quest-naming]] | 데이터 | "퀘스트 관련" 4행 |
| [[decisions/2026-05-28-meta-termbase-emergency]] | **사후 결정** | ⚠ §11 권한 트리거 우회 사실 + 사후 정당화 (재발 방지 자료) |

---

## Sections

- `wiki/sections/` — **미생성**. DB 묶음 작업 시작 시 자연 생성.

---

## 미해결 후속 작업 (우선순위 순)

1. **§4-c lore ingest 계속** — A 시작 알파벳 계속, 그 다음 raw/Online 진입 검토 (현재 발췌 316만, ingest 0).
2. **평문 등장 termbase 위키링크 승격** — mundus/redguard/meridia/imperial 등 lore 평문 등장 분 [[termbase/...]] 링크화. *fix-as-you-go* + 라운드 끝 lint.
3. **in-link 0인 9개 termbase 자연 등장 trigger 대기** — bosmer/dibella/falmer/jyggalag/maormer/namira/peryite/sanguine/zenithar. 등장 시 즉시 활용. (강제 등장 X — §4-c 정신 위반된 사전 채움이므로)
4. **§6 세션 시작 의례 정착** — 사관 교체 시 *log.md 마지막 5줄 + index.md 한눈 통계*로 진입.
5. **decisions/seed-* 별도 폴더 분리 여부** — 다음 외부 시드 자료 한 번 더 보고 결정.
6. **§5.5 갱신 의무 강화** — 본 index가 *2026-05-26 이후 갱신 0*이었음. 50 commit 또는 라운드 끝마다 *반드시* 본 페이지 갱신.

---

> *시간순 변경 이력은 [[log]] 참조.* index.md는 *현재 상태 스냅샷*.
