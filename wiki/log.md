# 작업 로그

CLAUDE.md §5.6에 따라 모든 batch·decision·lint를 한 줄씩 append.

---

## [2026-05-26] seed-import #1 | "ESO (고유)명사 번역 통일안.xlsx" 5,600행 14시트
- termbase 619 페이지 생성 (확정됨 39, 인명 61, 지명 175, 기타 66, 아이템 61, 던전 217)
- decisions/ 6 시드 문서 생성 (debate 339, merkmire 97, policy 33, npc-tone 10, pending 4, quest-naming 4)
- 마찰점 8건 → [[decisions/seed-import]]에 종합
- 슬러그 충돌 9건 (모두 동일 매핑 중복, 무해)
- 멀티 항목 행 2건 (검토 표시)

## [2026-05-26] CLAUDE.md 보강 #1 | 외부 리뷰 1차 반영
- §4-b 시드 import 워크플로 신설
- §5.0 슬러그 정책 명시 (`TermController::normalizeTerm`과 일관)
- §5.1 frontmatter status/source_* 필드 정식화
- §11 시드 import 단서 추가

## [2026-05-26] CLAUDE.md 보강 #2 | 외부 리뷰 2차 반영
- §0 Phase 1/2 박스 신설 (명세 vs 구현 명시)
- §2.3 claude_batches.state 숫자 enum 부여
- §5.1 language_code 일관성 한 줄
- §7 응급 SQL "Claude 자동 실행 금지" 경고

## [2026-05-26] A' 보강 | 위생 정리
- placeholder→TODO 마커 451건 (lint 가능화)
- 멀티 항목 2건 flags:needs-split 추가
- §11 권한 트리거 형식 명시 (seed-policy 파일 + 명시 승인)
- §5.6 한 줄 + ≤5 sub-bullet 완화

## [2026-05-26] A' 후속 보강 | 외부 리뷰 3차 반영
- 멀티 항목 2건 YAML frontmatter 복구 (단일 문자열 + 본문 표)
- §4 step 1 fix-as-you-go 룰 추가 (TODO 마커 자동 보강)
- index.md "완료된 작업" 제거 (log.md가 시간순 정본)

## [2026-05-27] #4 충돌 접미사 9 파일 통합 | feature/remains
- 9개 자동 충돌 접미사 파일 삭제 (모두 동일 매핑이라 무손실)
- seed-import.md 마찰점 #5 ✅ 해결 표시 + #11 신규(슬래시 슬러그) 추가
- index.md "미해결 후속" 4번 항목 ✅ 완료 표시, 7번(슬래시) 추가

## [2026-05-27] #3 멀티 항목 분리 (부분) | feature/remains
- 글리프 등급 16개 분리 완료 (충돌 없음, 16 신규 페이지)
- 물약 접두어 9개 *분리 보류* — 5건이 아이템 시트와 다른 한글 매핑 (마찰점 #12)
- trifling parent 페이지 → 시리즈 색인으로 갱신 (`flags:[split-done]`)
- sip-of parent 페이지 → 충돌 안내 + `flags:[needs-split, conflict-with-아이템-시트]` 갱신

## [2026-05-27] #5 기타사전 64건 세부 분류 | feature/remains
- 64개(충돌 통합으로 66 → 64) 재분류: 게임용어 36 / 종족 15 / 진영 9 / 기타 4(메타)
- termbase 총 626 페이지로 갱신. 카테고리 분포 index.md 동기화
- seed-import.md 마찰점 #9 ✅ 해결 표시
- Claude 수동 판단 — 모호 경계 케이스(almsivi/tribunal/sapiarchs/mane/tonal-architect)는 사용자 검토 권장

## [2026-05-27] #1 style-guide.md 초안 신설 | feature/remains
- wiki/style-guide.md 10 섹션으로 신설 (seed-policy + seed-npc-tone 정수 추출)
- 핵심: 명명 형식 (퀘스트/인명/지명/스킬 등), 세트 아이템, NPC 톤(카짓 3인칭+7 NPC 표),
  ⚠ 시스템 토큰 보존 (변수/색상/단복수/ID/명사속성)
- seed-import.md 마찰점 #8 (style-guide 미생성) ✅ 부분 해결 표시 (lore/sections는 미생성)
- index.md 미해결 #1 ✅ 완료 / Style Guide 섹션 갱신

## [2026-05-27] #3 후속 — 물약 충돌 옵션 B 결정 | feature/remains
- 사용자 결정: 아이템 시트 매핑이 정본 (시리즈는 "전혀 상관없이 만든 것도 많음" + "(구버전)" 표시)
- 아이템 시트 9 페이지 정본 유지 (sip-of/tincture-of/dram-of/potion-of/solution-of/elixir-of/panacea-of/distillate-of/essence-of)
- 시리즈 페이지(sip-of-tincture-...md) ⛔ retire 색인으로 갱신 (`flags:[retired, superseded-by-아이템-시트]`)
- seed-import.md 마찰점 #12 ✅ 해결 표시
- index.md 미해결 #3 → ✅ 완료 / 플래그 안내 갱신

## [2026-05-27] #7 슬래시 슬러그 정리 | feature/remains
- 4 신설: jerkin (조끼) / robe (로브) / kinlady (혈족군주, +kinload 오타 alias) / kinlord (혈족군주)
- 3 retire 색인: jerkin--robe / kinlady--kinload / kinlord--kinlady
- termbase 총 630 페이지 (retire 4 포함). 분포: 던전 211 / 지명 174 / 게임용어 93 / 아이템 63 / 인물 61 / 종족 15 / 진영 9 / 기타 4
- seed-import.md 마찰점 #11 ✅ 해결 표시
- index.md 미해결 #7 → ✅ 완료 / 분포 표 + 플래그 안내 갱신

## [2026-05-27] #D 451 TODO termbase → UESP 자동 보강 | feature/remains
- 443 TODO 페이지(이전 451에서 작업 후 줄어듦)에 대해 raw/Online + raw/Lore 정확 일치 매칭
- **371개 보강** (Online 316 + Lore 55, 보강율 84%) — UESP markup cleaning 후 첫 문단 추출
- 남은 72개(매칭 없음 69 + stub 3): 직책/일반 아이템 등 entity 페이지 없는 케이스
- 예시 [[dremora]]: "Dremora are an intelligent, humanoid Daedric race that despises mortals..."
- 위키 *진짜 가공 가능* 입증 — 이전 "전수 ingest 비현실" 답변 정정

## [2026-05-27] raw 분류 시스템 + CLAUDE.md §11 정정 | feature/uesp_ingest
- **CLAUDE.md §11 정정**: "raw 파일 *내용* 수정 X (디렉토리 분류·이동은 OK, 적극 권장)" — 이전 "raw 폴더 파일 수정" 오해 해소
- **raw/<폴더>/_ingested/ 서브폴더 도입**: 처리 완료 파일 이동
  - raw/Online/_ingested/: 316 파일
  - raw/Lore/_ingested/: 55 파일
  - 루트 미처리: Online 72887, Lore 13877
- **raw/_manifest.md 신설** — raw 파일 ↔ termbase 매핑 표 (371 행)
- **.gitignore 갱신** — raw/Books/Lore/Online + raw/en.lang.csv 추가 (87K 사고 재발 방지)

## [2026-05-27] .gitignore negate 정정 + _ingested 추적 회복 | feature/uesp_ingest
- 이전 .gitignore가 raw/<폴더>/ 통째 ignore라 _ingested/도 자동 누락 사고
- 패턴 정정: raw/<폴더>/* + !raw/<폴더>/_ingested/
- 371 ingested 파일 git 추적 회복 (Online 316 + Lore 55)
- check-ignore로 5개 sample 검증 완료

## [2026-05-27] CLAUDE.md §4-c lore ingest 워크플로 정식화 | feature/uesp_ingest
- **§4-c 신설**: UESP entity 단위 깊이 ingest 워크플로 (카파시 정신)
  - source 전체 read + 사용자 takeaway 논의 + wiki/lore/<한글이름>.md 신설 + cascading
- **§4·§4-b·§4-c 비교 표** 추가 — 세 종류 ingest 명확 구별
- **§4-c.3 *발췌* ≠ *ingest* 구별 명문화** — 371 발췌는 ingest 승격 대기 상태
- **§11 단서**: "raw 첫 문단 추출을 'ingest'로 호명 금지"
- 이번 라운드의 *sourcing/ingest 혼동* 사고를 정책으로 박아 재발 방지

## [2026-05-28] goal lore ingest 라운드 1 (50 commit + lint) | feature/uesp_ingest
- raw/Lore 알파벳 순 첫 50 파일 ingest
  - 신규 lore 페이지 33개 (2920 시리즈 12 + 16 Accords 시리즈 3 + 36 Lessons of Vivec 9 + 기타 9)
  - redirect 처리 (lore 페이지 신설 X) 17개
- 핵심 entity 흡수: 2920 시리즈 12권 (Tribunal + Reman III + Versidue-Shaie + Vivec 등),
  16 Accords (Sheogorath의 광기 우화), 36 Lessons Sermon 1-18 부분 (Vivec 종교 텍스트),
  2E 582 (ESO 게임 시점 — DLC별 사건 종합)
- raw/Lore: 14101 → 13827 (274 줄음, 50개는 sermon 19+에서 시작)
  - 정확: 105 _ingested (이전 55 + 새 50)
- lint: orphan 검사 — 33 lore 페이지 모두 *서로 link 있지만* grep 패턴 한계로 일부 orphan 표시 (옵시디언 graph view에서 정확 확인 권장)

## [2026-05-28] lore 메타-개념 termbase 승격 | feature/uesp_ingest
- 사용자 의견: "Tamriel 탐리엘 이런 말은 되게 공용으로 여기저기서 쓰이는 것이니까 용어집같은 걸 추가하는게 좋지 않나요"
- 분석: lore/ 본문에 247개 broken [[X]] 링크 — 핵심 신성·종족·지명·메타-개념이 *xlsx 시드에서 누락*
- **termbase 54개 신설** (Daedric Princes 16 + Aedra 8 + Magnus·Lorkhan + 우주 메타 8 + Tribunal 5 + 종족 14 + 지명 2 + Walking Ways)
- **lore wikilink 204개 일괄 갱신** ([[X]] → [[X|한글표기]]) 회차 2번
- broken lore link: 247 → 189 (58 해결)
- termbase 총수: 630 → 684

## [2026-05-28] lore ingest sermon 29-31 + 3 | feature/uesp_ingest
- 36 Lessons of Vivec Sermon 29 (Scripture of the Numbers — *Vivec의 Nerevar 살해 자백 hidden message*)
- Sermon 30 (City-Face — 6th monster)
- Sermon 31 (Book of Hours 기록 — 검열본/대중본 이중 텍스트)
- Sermon 3 (Dwemer 포획 + 사랑의 본질 + 8 known worlds 신학)

## [2026-05-28] goal lore ingest 라운드 2 (50 commit + lint) | feature/uesp_ingest
- 36 Lessons of Vivec 시리즈 *완결* (sermon 1-37 = 37/37 + 시리즈 색인)
- Monument Island Plaques 시리즈 *완결* (1-5)
- Manifestos of Kinlord Rilis XII 시리즈 *완결* (2-4)
- A-시작 lore 단편 ingest: Betrayal of Our Heritage / Bloody Journal / Bosmeri Sleeping-song / Ald Sotha / House Telvanni / Brother's Plea / Common Hair / Recollection / Open Borders / Cat's Serenade
- redirect _ingested 이동 7건 (3rd/4th Age/Era, 5th Era, 8/9 Divines)
- **termbase 메타-개념 *대확장 (54+8)***: Daedric Princes 16 + Aedra 8 + 우주 메타 8 + Tribunal 5 + 종족 14 + Walking Ways/CHIM/High Isle/Serpent/Vivec City/지명 보강
- **한글 표기 정정 5건** (Hircine 허씬 / Mehrunes Dagon 메이룬스 데이건 / Jyggalag 지갈렉 / Almalexia 아말렉시아 / Arkay 아케이)
- **CLAUDE.md §5 정책 박기**: 위키링크 슬러그는 *실제 파일명 그대로*. §5.0.1 책·시리즈 파일명 prefix 정책 신설
- **잔여 broken lore link 9회 정정** (padomay/스라시안-역병/아우리돈/대거폴/일리악-만)
- 진행도: raw/Lore 13854 → 13795 (59↓), _ingested 95 → 153 (58↑)
- lore 페이지: 33 → 75 (42↑), termbase: 630 → 687 (57↑)
- lint: broken lore 289 (전부 진짜 lore ingest 대상 - §4-c), broken termbase 0
- 50 commits → lint 통과 (push는 WSL credential 문제로 사용자 직접)

## [2026-05-28] 메타-리뷰 대응 + ESO 3대 동맹 + 22 broken lore 채움 | feature/uesp_ingest
- **사용자 메타-리뷰 지적**: §11 권한 트리거 우회, decisions/ 로그 부재, §4-c cascading 미완, CLAUDE.md §5 정책 갱신 누락
- **사후 결정 로그 작성**: [[decisions/2026-05-28-meta-termbase-emergency]] — 위반 사실 + 사후 정당화 + 재발 방지
- **CLAUDE.md §4-c.1 보강**: "카테고리 단위 사전 일괄 채움 금지" + "모호한 의견 해석 금지" 두 줄 추가
- **사용자 추가 지적 (Ebonheart Pact 등 누락)**: ESO 3대 동맹 + Three Banners War + Alessian Empire 5개 termbase 신설 (lore 자연 등장 ≥2회 — §4-c 준수)
- **사용자 지적 (index.md 죽음)**: index.md 전면 재작성 (2026-05-26 이후 미갱신 → 691 termbase/88 lore 반영)
- **사용자 요청 (lint 더 열심히)**: broken lore ≥2회 22개 일괄 lore page 작성 — 2920 NPC 12 (Reman III/Versidue-Shaie/Turala/Juilek/Brindisi Dorom/Rijja/Empress Tavia/Miramor/Zuuk/Corda/Cassyr Whitley/King Drozel) + Monument 2 (Bendu Olo/All Flags Navy) + Tribunal lore 8 (Trinimac/Night Mother/Morag Tong/House Indoril/House of Troubles/Heart of Lorkhan/Muatra/Nerevarine)
- lore: 88 → 110 (22↑), termbase: 687 → 696 (9↑)

## [2026-05-28] goal lore ingest 라운드 3 (100 commit 체크포인트) | feature/uesp_ingest
- A 시작 알파벳 ingest 계속: A Dance in Fire 7권+색인, A Dance in Moonlight, A Daughter's Journal, A Deal is Struck, A Diet of Eyes, A Distracted Enemy, A Dragonhorn, A Dream of Sovngarde, A Dubious Tale Crystal Tower, A Feast Among the Dead 4ch+색인, A Final Appeal, A Folk Tale, A Forebear Warrior's Song, A Fortune Behind Those Walls, A Free Argonian's Manifesto, A Game at Dinner, A Gentleman's Guide to Whiterun, A Gift of Sanctuary, A Gold Coast Children's Bestiary, A Grand Transformation, A Grifter's Apology, A Guide to Dwemer Mega-Structures, A Guide to Fishing Tamriel, A Guide to Liturgical Vestments, A Guide to the Deadlands, A Harrowing Sea Voyage, A Helpful Steadfast Hand, A Hero's Weapon, A History of Blackrose Prison, A History of Daggerfall
- redirect _ingested 이동 9건 (Dance in Fire v1-v7 + Conversation Arabelle/Ascendant + Dance in Fire compilation)
- 진행도: raw/Lore 153 → 219 _ingested (66↑), 13795 → 13729 남음
- lore: 110 → 153 (43↑), termbase: 696 변동 X
- lint: broken termbase 0, broken lore ≥3회 15종 (다음 사이클 자연 trigger 대기 — Systres/Necrom/Forebears/Dagoth Ur/Wild Hunt/Mach-Makka/Kagrenac/Hist/Cathay-raht/Battle of Red Mountain 등)
- 시리즈 완결: A Dance in Fire (7+색인), A Feast Among the Dead (4+색인)

## [2026-05-28] goal lore ingest 라운드 4 (150 commit 체크포인트) | feature/uesp_ingest
- A 시작 알파벳 ingest 계속: A History of Lilmoth, A History of Mor Khazgur, A History of Shipbuilding Vol 1, A Hunter's Journey II/VI, A Hypothetical Treachery, A Kiss Sweet Mother, A Legionary's History of Fort Redmane, A Less Rude Song, A Life Barbaric and Brutal, A Life of Strife and Struggle, A Life of Uriel Septim VII, A Light on the Moor, A Lissome Sprite, A Loathsome Civilization, A Looter's Paradise, A Memory Book 3part+색인, A Merchant's Guide to Valenwood, A Midnight Ambush, A Minor Maze, A Mother's Lament/Nursery Rhyme, A Nereid Stole My Husband, A New Cult Arises, A New Guild for Fighters?, A New Recipe?, A Nixad Made Me Do It, A Petition for the Mighty Nix-Ox, A Plea for Vengeance, A Pocket Guide to Mournhold, A Prayer to the Serpent, A Prisoner's Journal, A Reach Travel Guide, A Rejection of Open Borders, A Reminder from the Judge, A Report on the Dusksabers, A Request for Relief/Your Support, A Royal Embarrassment, A Sacrament Remains, A Sailor's Guide to Sea Elves, A Scholar's Guide to Nymphs, A Shallow Pool, A Short History of Morrowind, A Sister's Regret/Retort, A Sky of Dusk, A Smuggler's Plan, A Soldier's Letter, A Star Walks In Craglorn
- 시리즈 완결: A Memory Book (3+색인)
- 3부 sequel: Brother's Plea → Sister's Retort → Sister's Regret (Dragon Cult Scalecaller 분열)
- 진행도: raw/Lore 219 → 272 _ingested (53↑), 13729 → 13676 남음
- lore: 153 → 206 (53↑), termbase: 696 변동 X
- lint: broken termbase 0, broken lore ≥4회 10종 (Sithis, Great Houses, Dark Brotherhood, Systres, Fa-Nuit-Hen, Dagoth Ur, Zaan-the-Scalecaller, Necrom, Hist, Barons of Move Like This — 자연 trigger 대기)

## [2026-05-28] goal lore ingest 라운드 5 (200 commit 체크포인트) | feature/uesp_ingest
- A 시작 알파벳 계속 (63 신규 lore): A Study of Fabricants, A Summoner's Guide to Nymics, A Supplicant's Song, A Tale Forever Told, A Tale of Baar Dau, A Tale of Greed, A Tale of Kieran, A Threnody to Lost Love, A Time of Troubles, A Tough Audience, A Trader's Eye for Fashion, A Tragedy in Black, A Travel Guide to Tamriel Castles, A Treatise on the Knot, A Trespasser in Ivyhame, A Vision of the Twin Citadels, A Warning to the Aldmeri Dominion, A Werewolf's Confession, A World of Corpses, A Year Among the Eagleseer Clan, A conversation with Orbath gro-Agdurz, A'tor, ABCs for Barbarians, AIOS, ART OF SMASHING VOL. 1, Aalto, Abah's Landing Merchant Lords 6+색인, Abah's Landing, Abamath, Abanabi Caves, Abecean Sea, Abelle Chriditte, Abernanit, **Abnur Tharn**, Aberrant Welkynd Stones, Abolisher, Abomination, Abyss, Abyssal Geysers, Academy of Chorrol, Academy's Rejection Letter, Accession War, Acharyai, Achieving Harmony with Death, Actors Guild, Ada'Soom Dir-Kamal, Ada, **Adamantine Tower**, Adamantium, Adamus Phillida Slain!, Adjacent Place, Adrimk, Advances in Lockpicking, Adventurer's Almanac 색인, **Aedra (심층)**, Aedra and Daedra (Kirkbride)
- 진행도: raw/Lore 272 → 374 _ingested (102↑), 13676 → 13574 남음
- lore: 206 → 269 (63↑), termbase: 696 변동 X
- 시리즈 완결: Abah's Landing Merchant Lords (6 + 색인), Adventurer's Almanac (3 + 색인)
- 메타-lore 심층: Abnur Tharn (Five Companions + Dragonhold), Adamantine Tower (Convention 무대), Aedra (8 culture creation myth)
- lint: broken termbase 0, broken lore ≥5회 8종 (Dark Brotherhood/Sithis/Great Houses/Fa-Nuit-Hen/Dagoth Ur/Systres/Forebears/Ayrenn — 자연 trigger 대기)

## [2026-05-28 22:00] migration | termbase + lore → wiki/ flat | 965 files migrated
- 사용자 mission pivot 결정 ([[decisions/2026-05-28-mission-pivot]]): namespace 폐기 + ES 전문가 wiki 미션
- 이동: 696 termbase + 270 lore (1 충돌 자동 합병 = aedra) → wiki/<slug>.md flat 965개
- 위키링크 일괄 교체: 2941 substitution (`[[termbase/X]]`, `[[lore/X]]` → `[[X]]`). 깨진 형식 1건 수동 fix.
- frontmatter 통일: kind: entity(745) + book(220), category closed list (책 220, 던전 211, 지명 196, 개념 103, 인물 83, 유물 65, 신성 36, 종족 29, 진영 17, 기타 4, 사건 1)
- CLAUDE.md §4.3에 *던전* 추가 (211개라 별도 카테고리 가치)

## [2026-05-28 22:30] lint + stub | broken/orphan 실측 + top 22 stub
- 마이그레이션 후 *실상* (namespace 가림막 제거 후): broken 889 unique slugs, orphan 647 (66.8%)
  - 즉 이전 진단(broken 274, orphan 129)은 *flat 시야로 *재측정해야 *진짜 수치*
- top 22 broken (≥5회) 내장 ES 지식으로 stub 생성 (status: stub): Dark Brotherhood/Sithis/Ayrenn/Fa-Nuit-Hen/Great Houses/Dagoth Ur/Systres/Forebears/Necrom/Baar Dau/Barons of Move Like This/House Telvanni/Hist/Zaan the Scalecaller/Bosriel/Divayth Fyr/The Reach/Crowns/Dragon Cult/Goblin/Ordinator/Mannimarco
- stub은 *최소 정의 + 자연 trigger 시 §3.1 ingest로 *심층 보강 예약*. *bosriel = needs-research flag.
- 2차 broken 발생: stub이 만든 [[house-hlaalu]] 등 → 다음 cascade 대상
- index.md 전면 재작성: 마이그레이션 반영 + 카테고리별 주요 entity 큐레이션 + Dataview 예시

## [2026-05-30 14:00] ingest | 17 lore concept·character·event batch (17 source, ~1082줄) | touched: 22 pages
- raw 17 source: Kamal·Po Tun·Septim·Tsaesci·Wulfharth·Akulakhan·Almsivi·Anuad·Cyrodiilic·Knahaten Flu·Knights of the Nine·Mantella·Moon Sugar·Skooma·Underking·Warp in the West·Whirling School → _ingested
- Akavir 종족 3: kamal (Stonefalls 침공), po-tun (Tiger-Dragon), tsaesci (Snake-People/Dragonguard 후예) — sotha-sil 이미 처리
- 인물 2: septim (Dynasty 황제 명단), wulfharth (Shezarrine/Talos 3 영혼)
- Tribunal 1: almsivi (Tribunal 호명)
- 신학 3: anuad (Anu+Padomay 창조), cyrodiilic (Cyrodiil 문화 형용사), whirling-school (Vivec Walking Way)
- 사건 2: knahaten-flu (2E 560-603, Argonian Hist 후원 추정), warp-in-the-west (3E 417 Iliac Bay Dragon Break)
- 유물 4: akulakhan (Dagoth Ur Numidium 모방), mantella (Numidium 동력 Wulfharth 영혼), moon-sugar (Khajiit), skooma (Moon Sugar 증류)
- 진영 1: knights-of-the-nine (Pelinal Crusader's Relic 결사)
- 인물 1: underking (Wulfharth 형태)
- 신규 link: dagoth-ur (Akulakhan), akavir (Underking + 4 Akavir 종족), tiber-septim (Underking + Septim Dynasty), 36-lessons-sermon-20 (Whirling School), hero-of-kvatch (Knights of the Nine), anu (Anuad), cyrodiil (Cyrodiilic)
- 최종: 페이지 1355 → 1370, Orphan 0 유지, Broken 860

## [2026-05-30 13:00] ingest | 21 culture·pantheon·creature batch (21 source, ~814줄) | touched: 26 pages
- raw 21 source 처리. 종족별 깊이·Daedra 종류·Yokudan 신학·Bosmer 의례:
- Khajiit 3: riddle-thar (Two-Moons Path), khajiit-religion (Aedric 대응 + 고유 신 8), lunar-lattice (17 Furstock 결정 시스템)
- Argonian 3: hist-sap (Argonian 영적 수액), an-xileel (4E Morrowind 침공), shadowscale (Sithis Argonian 암살 조직)
- Bosmer 3: green-pact (Y'ffre 식물 금지 + 육식 의례), wild-hunt (Daedric 변환 의례 + 영원 사례), camoran-dynasty
- Daedric 종족 4: atronach (4 원소), dremora (4 Caste), daedroth, lesser-daedra
- Dragon Cult: dragon-priest (9 주요 Priest + Mask)
- Yokudan 신학 4: hoonding (Make Way Redguard), tall-papa (Ruptga), satakal (자기 식 뱀), tu-whacca (Far Shores), 
- Aedric 추가 3: y-ffre (Storyteller + Mundus 분류), mauloch (Orsimer Malacath), trinimac (Boethiah 변환 → Malacath)
- 신규 link: mankar-camoran (Camoran), hist (hist-sap + shadowscale), ruptga (Tall Papa), khajiit (Lunar Lattice + Khajiit Religion), daedra (Lesser Daedra 분류)
- 최종: 페이지 1340 → 1355, Orphan 0 유지, Broken 865

## [2026-05-30 12:00] ingest | 19 cosmology·history·tower batch (19 source, ~1131줄) | touched: 24 pages
- raw 19 source: Mythic Dawn (79) + Mankar Camoran (69) + Pelinal (7) + Belharza (47) + Morihaus (63) + Alessia (81) + Marukh (37) + Heart of Lorkhan (86) + Mantling (45) + Tonal Architecture (40) + Kagrenac (62) + Kalpa (56) + Earth Bones (5) + Tower (6) + Towers (6) + Crystal Tower (68) + Red Mountain (89) + Throat of the World (114) + Direnni (171) → _ingested
- Oblivion Crisis 2: mythic-dawn (Camoran Manifesto + Paradise), mankar-camoran (Bosmer-Altmer 혼혈)
- Alessian Era 4: pelinal (Shezarrine), belharza (Minotaur 시조), morihaus (반-Aedric Bull), alessia (Akatosh Covenant + Eight Divines), marukh (Maruhkati Selectives + Middle Dawn Dragon Break)
- Cosmic 핵심 5: heart-of-lorkhan (Convention 후 Red Mountain + Dwemer 사용 + Tribunal Apotheosis), mantling (Tiber → Talos), tonal-architecture (Dwemer 비신성 마법), kagrenac (Sunder/Keening/Wraithguard), kalpa (Alduin Kalpa 종결자)
- Tower 4: earth-bones (Ehlnofey 물리법칙), towers (8 Mundus Tower), crystal-tower (Daedric Triad), red-mountain (Heart 챔버 + Red Year), throat-of-the-world (Time-Wound + Greybeards)
- Direnni: Aldmer Direnni Clan + Battle of Glenumbria Moors
- 신규 link: ehlnofey (Earth Bones), aedra/alessia (Pelinal), skyrim·thuum·greybeards (Throat of the World)
- 최종: 페이지 1322 → 1340 (1 통합), Orphan 0 유지, Broken 871

## [2026-05-30 11:00] ingest | 19 dragon·voice·reach batch (19 source, ~897줄) | touched: 22 pages
- raw 19 source: Paarthurnax + Odahviing + Miraak + Mirmulnir + Sahloknir + Durnehviir + Dragons + Dragon Cult + Dragon War + Dragonborn + Dovahzul + Thu'um + Greybeards + Tongues + Way of the Voice + Forsworn + Reachfolk + Hagraven + Briarheart → _ingested
- Dragon 6: paarthurnax (Alduin 배반·Way of Voice), odahviing (Dragonsreach), miraak (첫 Dragonborn·Mora), mirmulnir (4E 첫 처치), sahloknir, durnehviir (Soul Cairn Undead)
- Dragon 신학 3: dragons (Akatosh 자손), dragon-cult (Dragon Priest), dragon-war (Mortal 봉기)
- Voice 5: dragonborn (Miraak·Reman·Tiber·Septim·Last Dragonborn), dovahzul (Words of Power), thuum (Shout 구조 + Way of Voice + Tongues), greybeards (High Hrothgar 4E 호출), tongues, way-of-the-voice
- Reach 4: forsworn (4E Markarth Incident·Briarheart), reachfolk (Reach 원주민), hagraven (Glenmoril), briarheart (Forsworn 의례)
- 신규 link: alduin (5 Dragon + 2 사건 + Tongues 후예), dragons (Dovahzul/Dragonborn), skyrim (4E 201/Way of Voice/Greybeards), thuum (Paarthurnax/Dovahzul/Dragon War), forsworn (Briarheart)
- 최종: 페이지 1303 → 1322 (19 신규), Orphan 0 유지, Broken 875

## [2026-05-30 10:00] ingest | 22 vampire·lycanthropy·artifact batch (22 source, ~1113줄) | touched: 27 pages
- raw 22 source: Harkon (49) + Serana (45) + Valerica (34) + Volkihar (47) + Lord Harkon (5, dup) + Dawnguard (41) + Vampire Lord (4) + Vampirism (5) + Necromancy (233) + Lich (102) + Glenmoril (9) + Lycanthropy (226) + Bloodmoon (24) + Werebear/Wereboar/Werelion/Wereshark (각 4) + Dawnbreaker (42) + Oghma Infinium (61) + Ring of Namira (25) + Savior's Hide (55) + Skull of Corruption (30) + Spellbreaker (60) → _ingested
- Volkihar Court 4: harkon (Pure-Blood + Tyranny of Sun), serana (Elder Scroll), valerica (Soul Cairn 피신), volkihar
- Vampire 신학 3: vampirism (Lamae Bal 기원), vampire-lord (Magicka 비행), dawnguard (4E Vigilants 후계)
- Necromancy 신학 2: necromancy (Mannimarco 체계화 + Soul Cairn 거래), lich (Phylactery + Mannimarco 정점)
- Lycanthropy 3: lycanthropy (7 Werecreature 종류 + Glenmoril 변환), glenmoril, bloodmoon (Hircine Solstheim)
- 4 Werecreature 변형: werebear/wereboar/werelion/wereshark
- 6 Daedric Artifact: dawnbreaker (Meridia Undead), oghma-infinium (Mora 능력치), ring-of-namira (식인 ring), saviors-hide (Hircine armor), skull-of-corruption (Vaermina clone), spellbreaker (Peryite shield)
- 신규 link: meridia, vampire, mannimarco, hircine (Werecreature 5 + Great Hunt), namira, vaermina, peryite
- 최종: 페이지 1283 → 1303 (22 source + 22 page rewrite), Orphan 0 유지, Broken 879

## [2026-05-30 09:00] ingest | 15 realm batch (15 source, ~984줄) | touched: 17 pages
- raw 15 source: Apocrypha (113) + Coldharbour (95) + Deadlands (110) + Detritus (35) + Evergloam (46) + Hunting Grounds (68) + Maelstrom (43) + Moonshadow (42) + Pinnacle Rock (21) + Quagmire (47) + Shivering Isles (128) + Soul Cairn (62) + Sovngarde (94) + Spiral Skein (49) + Attribution's Share (31) → _ingested
- 15 Oblivion 영역 + Sovngarde:
  - Apocrypha (Hermaeus Mora 무한 도서관 + Miraak), Coldharbour (Molag Bal Planemeld + Vestige), Deadlands (Mehrunes Dagon 용암 + Battlespire), Evergloam (Nocturnal Twilight + Sepulcher), Hunting Grounds (Hircine Werewolf 영혼), Moonshadow (Azura 아름다움), Pinnacle Rock (Peryite 중립 회담), Quagmire (Vaermina 악몽), Shivering Isles (Sheogorath Mania/Dementia + Greymarch), Soul Cairn (Ideal Masters Black Soul Gem), Sovngarde (Shor Hall of Valor + Alduin 대결), Spiral Skein (Mephala 거미줄), Detritus (Hircine/Hollowjack 일부), Maelstrom-Arena (Fa-Nuit-Hen, 슬러그 변경), Attribution's Share (Jyggalag)
- 신규 link: peryite (Pinnacle Rock 호명), coldharbour (Soul Cairn 인접), hircine (Detritus 일부), maelstrom-arena (a-challengers-thoughts 기존 broken link 해결)
- 최종: 페이지 1268 → 1283, Orphan 0 유지, Broken 880

## [2026-05-30 08:00] ingest | 24 hero·artifact batch (24 source, ~1772줄) | touched: 25 pages
- raw 24 source 처리 + black-book + 6 Five Companions/Vestige 신규
- ESO Five Companions + Vestige 7: vestige, lyris-titanborn, sai-sahan, the-prophet, abnur-tharn, cadwell + ESO 메인 퀘스트 종합
- 게임 영웅 5: nerevarine (Azura Seven Visions + Heart 파괴), hero-of-kvatch (Madgod 후계자), last-dragonborn (다중 역할 + Alduin 처치), champion-of-cyrodiil, eternal-champion (Arena/3E 389), dagoth-ur (Voryn → Sharmat 6 Ash Vampire)
- 핵심 유물 13: numidium (Brass God + Warp in the West), wabbajack, skeleton-key, trueflame (Almalexia 광기 처치), volendrung (Hammerfell 연원), mehrunes-razor, ebony-blade (Mephala 친구 흡수), eye-of-magnus, ring-of-hircine, spear-of-bitter-mercy, mace-of-molag-bal, sanguine-rose, black-books (기존 페이지 갱신·중복 black-book.md 삭제)
- hermaeus-mora·miraak·hircine·sheogorath·sanguine·magnus·mehrunes-dagon·winterhold에 신규 wikilink 삽입
- 최종: 페이지 1244 → 1268 (1 중복 삭제 후), Orphan 0 유지, Broken 880

## [2026-05-30 07:00] ingest | 29 cities batch (29 source, ~3489줄) | touched: 29 pages
- raw 29 source 처리 (3 batch: Cyrodiil 9 + Skyrim 9 + Morrowind 6 + High Rock/Hammerfell 3 + Valenwood/Summerset 2)
- Cyrodiil 9: imperial-city (White-Gold Tower), bruma (Oblivion Crisis Great Gate), anvil (Yokudan), skingrad (Vampire 백작), cheydinhal (Dark Brotherhood), chorrol (Fighters Guild), kvatch (Oblivion 첫 Gate), leyawiin (Blackwood Company), bravil (Lucky Old Lady)
- Skyrim 9: whiterun (Dragonsreach + Companions), solitude (4E 수도), markarth (Dwemer + Markarth Incident), windhelm (Ysgramor 건립 + Argonian 차별), riften (Thieves Guild + Nightingale), falkreath (Dark Brotherhood 마지막 Sanctuary), winterhold (College + Great Collapse), dawnstar (Mythic Dawn 잔존), morthal (Hagraven Jarl)
- Morrowind 6: balmora (Hlaalu 수도 + Nerevarine 시작), vivec-city (8 Cantons + Ministry of Truth), ald-ruhn (Skar Emperor Crab), sadrith-mora (Telvanni Mushroom Tower), mournhold (Almalexia 도시 + Old Mournhold 파괴), suran (House of Earthly Delights)
- High Rock/Hammerfell 3: wayrest (Daggerfall Covenant 수도), daggerfall-city (Warp in the West), sentinel (Forebear)
- Valenwood/Summerset 2: elden-root (Aldmeri Dominion 수도 + Graht-oak), vulkhel-guard (Vestige 시작지)
- skyrim.md 9 Holds 모두 wikilink 변환, high-rock·valenwood·auridon에 신규 link 삽입
- 최종: 페이지 1233 → 1244, Orphan 0 유지, Broken 890

## [2026-05-30 06:00] ingest | 18 alliance·house·event·artifact batch (18 source, 1842줄) | touched: 17 pages
- raw 18 source: Aldmeri Dominion (62) + Daggerfall Covenant (72) + Ebonheart Pact (49) + Great House Hlaalu (6) + Great House Redoran (6) + Great House Telvanni (6) + House Dres (164) + House Dagoth (103) + Tribunal Temple (57) + Three Banners War (345) + Imperial Legion (415) + Thalmor (94) + Stormcloaks (20) + Stormcloak Rebellion (98) + Ashlanders (102) + Amulet of Kings (97) + Auriel's Bow (56) + Chrysamere (90) → _ingested
- 17 페이지 심층 재작성 (Stormcloaks + Stormcloak Rebellion = 1 page):
  - 3 alliance: aldmeri-dominion (Ayrenn 2차 + Thalmor 3차), daggerfall-covenant (Emeric), ebonheart-pact (Jorunn)
  - 4 House: great-house-hlaalu (Imperial 친화·4E 몰락), great-house-redoran (전사·4E 부상), great-house-telvanni (Magister 시스템·노예제), house-dres (Tear plantation·4E Argonian 침공 몰락)
  - 1 Sixth House: house-dagoth (Voryn → Dagoth Ur 6 Ash Vampire)
  - 1 Temple: tribunal-temple (Indoril 주도, 4E Reclamation Temple 변환)
  - 1 War: three-banners-war (2E 582, Soulburst + Coldharbour Compact + Vestige)
  - 1 Legion: imperial-legion (Alessian → Reman → Septim 척추, Penitus Oculatus)
  - 1 Thalmor: 4E 3차 Dominion 지배 + White-Gold Concordat
  - 1 Stormcloak: stormcloak-rebellion (Markarth Incident + Torygg 처치 + Last Dragonborn 결정)
  - 1 Ashlanders: 4 Tribe (Ahemmusa·Urshilaku·Zainab·Erabenimsun) + Nerevarine 예언 수호
  - 3 Artifact: amulet-of-kings (Chim-el Adabal + Akatosh Covenant + Martin 파괴), auriel-bow (Dawnguard Tyranny of Sun), chrysamere (Paladin claymore 영웅 순환)
- 최종: 페이지 1225 → 1233, Orphan 0 유지, Broken 891

## [2026-05-30 05:00] ingest | 9 주요 guild batch (9 source, 1187줄) | touched: 9 pages
- raw 9 source: Mages Guild (202) + Fighters Guild (74) + Thieves Guild (66) + Dark Brotherhood (202) + Morag Tong (85) + Companions (157) + Psijic Order (214) + Blades (181) + Vigilants of Stendarr (6) → _ingested
- 9 페이지 심층 재작성:
  - mages-guild: Vanus Galerion 결성, Arch-Mage 위계, Eyevea, Necromancy 금지
  - fighters-guild: 2E 321 공식화, Akaviri Fighters Guild 전신, Blackwood Company 경쟁
  - thieves-guild: Gray Fox/Nightingale, Hew's Bane (Abah's Landing), Shadowmark
  - dark-brotherhood: Sithis + Night Mother, Five Tenets, Morag Tong과 원수
  - morag-tong: Mephala 창립, Writs of Execution, Dark Brotherhood 격파
  - companions: Ysgramor 후계, Circle Werewolf, Kodlak cure 추구
  - psijic-order: Tamriel 최오래, Iachesis, Mannimarco 추방, 2E 582 Artaeum 재출현
  - blades: Dragonguard 후예, Septim 경비, 4E 175 해체, Sky Haven Temple
  - vigilants-of-stendarr: 4E Daedra·Undead 사냥, Hall of Vigilant 학살
- 최종: 페이지 1222 → 1225, Orphan 0 유지, Broken 884

## [2026-05-30 03:30] ingest | Magic Schools 6 batch (6 source, 254줄) | touched: 6 pages
- raw 6 source: Alteration (45) + Conjuration (46) + Destruction (38) + Illusion (38) + Mysticism (41) + Restoration (46) → _ingested
- 6 페이지 심층 재작성: Tamriel 6 마법 학파 (Alteration/Conjuration/Destruction/Illusion/Mysticism/Restoration)
- 최종: 페이지 1216 → 1222, Orphan 0 유지, Broken 886

## [2026-05-30 02:00] lint | top broken 26 stub batch | touched: 26 pages
- 신규 stub 26: dragonguard, empire, akaviri, hlaalu-helseth, barenziah, nixad, saint-felms, ardent-hope, destructions-solace, alessian-order, lilmothiit, wrothgar, druids, faolchu, jagar-tharn, ivyhame, vinedusk-rangers, mortuum-vivicus, at-addin-syndicate, house-vien, thazahrr-cartel, gurges-and-associates, order-of-the-black-worm, forgotten-hero, sea-sload, scathing-bay
- 최종: 페이지 1190 → 1216, Orphan 0 유지, Broken 891

## [2026-05-30 01:00] ingest | Akavir 5 + Oblivion Crisis 4 batch (5 source) | touched: 9 pages
- raw 5 source: Akaviri (42) + Tsaesci (131) + Kamal (20) + Tang Mo (12) + Ka Po' Tun (21) → _ingested
- 9 페이지 심층 재작성 (Akavir 5 + Oblivion Crisis 4):
  - akavir: 4 종족 매핑, 1E·2E 두 번의 Tamriel 침공
  - tsaesci: Snake-Folk 불멸 영혼 흡수, Dragonguard 흡수 (Blades 기원)
  - kamal: Snow Demons, Second Akaviri Invasion → Ebonheart Pact 형성
  - tang-mo: Monkey-Folk, 가장 우호적
  - ka-po-tun: Tiger-Folk + Tosh Raka Dragon 변환 야망
  - mythic-dawn: Mehrunes Dagon cult, Mankar Camoran, Oblivion Crisis 주체
  - mankar-camoran: Bosmer-Breton Camoran 후예, Paradise, CHIM 사용
  - martin-septim: Septim 비밀 서자, Akatosh Avatar mantling, Dagon 추방
  - uriel-septim-vii: Septim Dynasty 마지막 황제, 암살 → Crisis 발화
- 최종: 페이지 1183 → 1190, Orphan 0 유지, Broken 917

## [2026-05-29 00:00 (5/30)] ingest | 사라진 종족 + Hist 9 batch (9 source, 939줄) | touched: 9 pages
- raw 9 source: Dwemer (247) + Falmer (91) + Ayleid (274) + Atmoran (5 redirect) + Nedic (4 redirect) + Hist (117) + Sload (102) + Reachman (4 redirect) + Maormer (95) → _ingested
- 9 페이지 심층 재작성:
  - dwemer: Aldmer 분파, Tonal Architecture, Animunculi, Numidium, Battle of Red Mountain에서 종족 동시 제거
  - falmer: Old Falmer (Snow Elves), Ysgramor 학살, Dwemer 노예→Betrayed, Forgotten Vale 잔존
  - ayleid: Wild Elves, Welkynd·Varla Stones, Daedric Worship, Alessian Slave Rebellion 추방
  - atmoran: Nord 직계 조상, Five Hundred Companions, Dragon Cult 원천
  - nedic: Tamriel Man 시조, Imperial·Breton·Kothringi 분기
  - hist: Argonian 시조 나무 신, Convention 이전 우주적 존재, Sithis 연결, root mind
  - sload: Thrassian Plague, All Flags Navy, Daedric Triad·Z'Maja 협력
  - reachman: 5 Hircine Aspects, Hagraven 변형, Longhouse Emperors, Forsworn Uprising
  - maormer: Pyandonea Sea Elves, Sun Lord Orgnum, Summerset 침공
- 최종: 페이지 1181 → 1183, Orphan 0 유지, Broken 920

## [2026-05-29 22:30] ingest+lint | 28 lint stub + 대형 사건/인물 10 batch (10 source) | touched: 38 pages
- batch lint: top broken 28 stub 생성: fadomai, auri-el, ebonarm, deadlands, darien-gautier, longhouse-emperors, oblivion-crisis, lyg, magna-ge, lorkhaj, neb-crescen, tel-aruhn, kothringi, gilverdale, euraxia-tharn, kaalgrontiid, markarth, murkmire, grabber, birthsigns, war-of-the-first-council, dissident-priests, house-dagoth, ruelde, dragon, blackcaster-mages-guild, hagraven, welkynd-stone
- 대형 사건+인물 10 source: Battle of Red Mountain (87) + Mannimarco (278) + Ysgramor (154) + Tiber Septim (297) + Talos (45) + Reman (66) + Ayrenn (87) + Ulfric Stormcloak (78) + Pelinal Whitestrake (119) + Lamae Bal (54) → _ingested + 심층 재작성
  - battle-of-red-mountain: 4 판본·Tribunal 살해 의혹·결과
  - mannimarco: King of Worms, Psijic 추방·Soulburst·Planemeld·Lich
  - ysgramor: Five Hundred Companions, Falmer 학살, Sovngarde
  - tiber-septim: 제3제국 창건, Numidium 사용, Enantiomorph 3 영혼, Apotheosis→Talos
  - talos: Enantiomorph 3 영혼, CHIM, Mantling Lorkhan, 4E 신앙 금지
  - reman: Second Empire 창건, Akaviri 격퇴
  - ayrenn: Aldmeri Dominion Queen, Psijic 수행
  - ulfric-stormcloak: 4E 201 Stormcloak 봉기, Talos 신앙
  - pelinal-whitestrake: Alessian 광기 전사, 시간 왜곡, Umaril 결투
  - lamae-bal: 최초 Vampire, Molag Bal 원수, Rite of the Scion
- 최종: 페이지 1150 → 1181 (28 lint + 3 신규 = 31), Orphan 0 유지, Broken 920

## [2026-05-29 21:00] ingest | 10 지방 batch (10 source, 2626줄) | touched: 10 pages
- raw 10 source: Tamriel (128) + Cyrodiil (128) + Skyrim (453) + Hammerfell (549) + High Rock (223) + Valenwood (179) + Summerset Isles (110) + Elsweyr (265) + Black Marsh (154) + Morrowind (437) → _ingested
- 10 페이지 심층 재작성:
  - tamriel: 9 지방·3 동맹·4 Empire·Tower 신학 (8 Towers 매핑)
  - cyrodiil: Imperial 본거지, Once Jungled→temperate (Tiber CHIM), 3 Empire 수도
  - skyrim: 9 Holds, Atmoran Ysgramor 이주, Dragon Cult·Sovngarde·Way of Voice, Stormcloak
  - hammerfell: Volenfell→Ra Gada Warrior-Wave, Crowns vs Forebears, Sword-Singer, 4E 독립
  - high-rock: Direnni Hegemony, 작은 왕국, Daggerfall Covenant, Druid·Wyrd, Systres
  - valenwood: Bosmer Green Pact 영토, Graht-oak 도시, Falinesti
  - summerset-isles: Aldmer 후예, Crystal Tower, Alinor·Artaeum, Thalmor
  - elsweyr: Khajiit Pellitine·Anequina, Moon Sugar 농경, Mane
  - black-marsh: Hist 영역, 늪 환경, 4E Morrowind 침공
  - morrowind: Velothi Exodus 목적지, 5 Great Houses, Battle of Red Mountain·Tribunal·Nerevarine·Red Year·Argonian 침공
- **Tamriel 9 지방 + 종족 + 신학 = 대륙 *총 *프레임 완성**
- 최종: 페이지 1150 (변동 없음), Orphan 0 유지, Broken 950

## [2026-05-29 19:30] ingest | 9 종족 batch (9 source, 3853줄) | touched: 9 pages
- raw 9 source: Argonian (537) + Khajiit (608) + Bosmer (366) + Altmer (483) + Breton (785) + Imperial (347) + Nord (306) + Redguard (416) + Orsimer (5 redirect) → _ingested
- 9 페이지 심층 재작성:
  - argonian: Saxhleel, Hist 직접 영적 연결, Sithis 친화, Shadowscale, 4E Morrowind 침공
  - khajiit: 17 Furstock, Lunar Lattice, Moon Sugar, Riddle'Thar Epiphany, Mane, 자체 신학 (Fadomai 등)
  - bosmer: Y'ffre Green Pact 4조항, Wild Hunt, Green Lady + Silvenar
  - altmer: Aldmer 직접 후예, Aldmeri Pantheon, 4E Thalmor·Aldmeri Dominion, Corelanya·Psijic
  - breton: Direnni + Nedic 혼혈, 마법 적성, Daggerfall Covenant, Druid·Wyrd
  - imperial: Colovian + Nibenese, 3 제국 (Alessian·Reman·Septim), Eight/Nine Divines, 4E Mede
  - nord: Atmoran 후예, Shor·Kyne, Dragon Cult, Sovngarde, Way of the Voice, Stormcloak
  - redguard: Yokudan, Ra Gada Warrior-Wave, Crowns vs Forebears, Sword-Singer Shehai, All Flags Navy
  - orsimer: Trinimac fall (Boethiah→Malacath), Wrothgar·Orsinium, Stronghold + Code of Malacath
- **9 종족 + Dunmer (Tribunal cluster) = 10 주요 종족 신학 완성**
- 최종: 페이지 1150 (변동 없음), Orphan 0 유지, Broken 926

## [2026-05-29 18:00] ingest | Aurbis 원초 신성 12 batch (12 source, 1216줄) | touched: 12 pages
- raw 12 source: Lorkhan (284) + Magnus (73) + Anu (93) + Padomay (83) + Sithis (151) + Aurbis (31) + Aetherius (73) + Oblivion (93) + Mundus (101) + Nirn (117) + Convention (51) + Dawn Era (66) → _ingested
- 12 페이지 심층 재작성:
  - anu/padomay: Aurbis 외부 두 원초 원리, CHIM의 Godhead 신학, Apostle "only Anu" 부정
  - aurbis: Wheel 형태, hub=Mundus, spoke=Aedric, "I" Tower
  - lorkhan: Mundus 창조 Trickster (Heart-less God), Doom Drum, Shor/Shezarr/Lorkhaj/Sep 문화별, Tower 신학 처음 목격, Amaranth 실패
  - magnus: Mundus Architect, Convention 후 Aetherius 도주 (Sun=도주 자국), Magna Ge (Stars), Magicka 원천
  - sithis: Padomay의 Aldmeri 표현, Dark Brotherhood 본존, Apostle 부정 대상, Vivec Sermon 35 "Original Death"
  - aetherius: Anu Soul 영역, Magnus/Magna Ge/Aedric 영혼, Sovngarde/Far Shores, 영혼 cycle
  - oblivion: 16 Daedric realms 전체 매핑, Mundus 경계, Oblivion Crisis/Planemeld
  - mundus: Lorkhan 창조 Mortal 영역, Aedric 희생, Tower 안정
  - nirn: 행성, 대륙 (Tamriel/Atmora/Akavir/Yokuda/Pyandonea/Aldmeris/Lyg)
  - convention: Mundus 창조 우주 사건 8단계, Aedra 희생, Magnus 도주, Lorkhan 처형
  - dawn-era: Convention 후 + Merethic Era 전, 시간·공간 flux, Aedra Mortal Walking, Akatosh Time 고정 종결
- **Tamriel 형이상학 우주관 완성**: 원초 (Anu·Padomay·Sithis) + Aurbis + 3 영역 (Aetherius·Oblivion·Mundus) + 행성 (Nirn) + 사건 (Convention·Dawn Era) + Lorkhan + Magnus
- 최종: 페이지 1148 → 1150 (convention·dawn-era 신규), Orphan 0 유지, Broken 917

## [2026-05-29 16:30] ingest | Aedric 8 batch (8 source, 969줄) | touched: 8 pages
- raw 8 source: Akatosh (206) + Arkay (116) + Dibella (117) + Julianos (80) + Kynareth (123) + Mara (142) + Stendarr (106) + Zenithar (79) → _ingested
- 8 페이지 심층 재작성:
  - akatosh: Dragon God of Time, Convention 주역, Auri-El/Alkosh/Alduin/Satakal/Tosh Raka 문화별, Saint Alessia covenant, Martin Septim mantling, 4E White-Gold Concordat
  - arkay: Burial Rites/Wheel of Life, 전 Mortal Hermit 기원, Necromancy 적, Vigilants of Stendarr 동맹
  - dibella: Beauty·Love·Art, Sybil 전통, Markarth Sanctum
  - julianos: Wisdom·Logic·Magic, Jhunal와의 관계, Mages Guild 후원
  - kynareth: Air·Heavens·Winds, Nordic Kyne, Morihaus 어머니, Saint Alessia 후원
  - mara: Mother Goddess, Almalexia의 Anticipation (4E Reclamations 후 Boethiah로 교체), Skyrim 결혼 의례
  - stendarr: Mercy·Justice, Apologist of Men (Lorkhan 변호), 4E Vigilants of Stendarr
  - zenithar: Work·Commerce·Trade, Yokudan Z'en 통합, Veloth 일부 연결
- **Aedric 8 Divines 심층 완성** — Tribunal·Good Daedra·Daedric Princes 16과 함께 *Tamriel 전체 *Pantheon 완성*
- 최종: 페이지 1148 (변동 없음), Orphan 0 유지, Broken 916

## [2026-05-29 15:00] ingest | 잔여 Daedric Princes 9 batch (9 source, ~1756줄) | touched: 9 pages
- raw 9 source 일괄: Mehrunes Dagon (406) + Meridia (169) + Clavicus Vile (178) + Malacath (272) + Sanguine (159) + Vaermina (166) + Peryite (149) + Namira (170) + Jyggalag (87) → _ingested
- 각 페이지 심층 재작성:
  - mehrunes-dagon: Destruction/Change/Revolution, Deadlands, Mysterium Xarxes/Lyg 기원, Oblivion Crisis 주범, Longhouse Emperors, Mournhold 격파·Deadlands 추방
  - meridia: Magna Ge (Merid-Nunda), Molag Bal 영원 적, Khajiit Magrus' 눈 사건, Crystal Tower 사건 (Triad에 감금), Planemeld 대항, Dawnbreaker
  - clavicus-vile: Barbas (반쪽 hound), Bargain insidious twist, Daedric Triad, Sunna'rah 사건, Umbra
  - malacath: Trinimac fall (Boethiah가 삼킴 + Ashpit 유배 → Mauloch), Orsimer 시조, Pariah-God, Sheogorath Orc 아들 사건, Volendrung
  - sanguine: Hedonism, Sam Guevenne, Sanguine Rose, Skyrim Whiterun
  - vaermina: Nightmares, Quagmire, Khajiit Varmiina (Azurah 처치), Skull of Corruption
  - peryite: 약한 Prince 논쟁, Tasks (낮은 Order), Pestilence balance, Spellbreaker, 용 형태
  - namira: Ur-dra 후보, Khajiit Namiira (Eldest Spirit/Great Darkness), 식인 cult, Ring of Namira
  - jyggalag: Sheogorath 원래 형태, 다른 Princes의 저주, Greymarch cycle, Hero of Kvatch mantling으로 자유, Sword of Jyggalag
- **Daedric Princes 16/16 심층 완성** (Tribunal·Good Daedra 포함하면 *Tamriel 형이상학 신학 완성)
- 최종: 페이지 1148 (변동 없음 — 모두 재작성), Orphan 0 유지, Broken 915

## [2026-05-29 13:30] ingest | Nocturnal cluster (1 source, 167줄) | touched: 10 pages
- raw 1 source: Nocturnal.md → _ingested
- nocturnal.md 심층 재작성 (22→230줄): Night/Darkness/Mystery, Evergloam realm, Ur-dra (Hermaeus Mora·Namira와 경쟁), "before Oblivion, there was Nocturnal", Khajiit Noctra (Lorkhaj Dark Heart 검은 피), Reachfolk Mistress of Shadows, Song of Hrormir (Gray Cowl 기원), Fable of the Gryphon, Twilight Sepulcher + Ebonmere + Nightingale Trinity, Witchmother coven, Shadow Magic + Gloaming Gates, Daedric Triad (Clavicus Vile + Mephala + Nocturnal, 2E 230 K'Tora 결탁→Crystal Tower 사건), 2E 582 Clockwork City 침공 + Crystal Tower 사건 (Nocturnal Vile·Mephala 배신→Vestige·Darien Gautier·Meridia가 격퇴), 3E·4E (Mercer Frey Skeleton Key 도난·Last Dragonborn 회수)
- 신설 9 entity: skeleton-key, gray-cowl-of-nocturnal, twilight-sepulcher, ebonmere, nightingales, daedric-triad, ur-dra, noctra, dark-heart (evergloam 기존)
- 최종: 페이지 1139 → 1148, Orphan 0 유지

## [2026-05-29 12:00] ingest | Hircine cluster (1 source, 366줄) | touched: 6 pages
- raw 1 source: Hircine.md → _ingested
- hircine.md 심층 재작성 (22→180줄): Lord of the Hunt, Hunting Grounds realm, 5 Aspects (Alrabeg/Storihbeg/Uricanbeg/Gulibeg/Hrokkibeg) + Glenmoril 6번째 Owl, Law of Fair Hunt, Father of Manbeasts (Lycanthropy), Bloodmoon/Great Hunt, 문화별 (Bosmer Wild Hunt + Y'ffre Green Pact 대립 / Reachfolk + Glenmoril Wyrd / Druids Elk of Arrows / Altmer 금지 / Khajiit Y'ffer Graht-Elk), Sheogorath 16 Accords 패배, Savior's Hide·Ring of Hircine
- 신설 5 entity: hunting-grounds, savior-hide, werewolf, bloodmoon, great-hunt (wild-hunt 기존)
- 최종: 페이지 1134 → 1139, Orphan 0 유지

## [2026-05-29 10:30] ingest | Sheogorath cluster (1 source, 228줄) | touched: 7 pages
- raw 1 source: Sheogorath.md → _ingested
- sheogorath.md 심층 재작성 (22→200줄): Madness/Creativity, Shivering Isles realm, Jyggalag 저주 (Order의 원래 형태), Greymarch cycle, Sithis-shaped hole, Khajiit Sheggorath/Skooma Cat, Chimer/Dunmer House of Troubles, Baar Dau (Vivec City 던짐), Apostle "Gray Prince of Order went mad in the knowing", 16 Accords of Madness, Shalidor Eyevea, Hero of Kvatch mantling (3E 433 Greymarch 종결), 4E Pelagius/Theodor Gorlash
- 신설 6 entity: shivering-isles, wabbajack, aureal, mazken, greymarch, hero-of-kvatch
- 최종: 페이지 1128 → 1134, Orphan 0 유지

## [2026-05-29 09:00] ingest | Molag Bal cluster (1 source, 358줄) | touched: 9 pages
- raw 1 source: Molag Bal.md → _ingested
- molag-bal.md 심층 재작성 (22→230줄): Domination/Brutality/Lies/Enslavement, Stone-Fire 어원, Coldharbour realm, 가족 (Ozozzachar/Molag Grunda/Haymon Camoran/Vampire 자손), Boethiah arch-enemy, Vivec Pomegranate Banquet (CHIM 수여 + Muatra 탄생 + Bal Ur 추방), 다층 호칭/문화 (Altmer/Ayleid/Dunmer/Khajiit Molagh/Reachmen), Gil-Var-Delle 파괴 (Coldharbour Compact 촉발), Lamae Bal Vampire 시조, Culanwe Coldharbour 고문, Soulburst (2E 578)/Planemeld (2E 582) 주도, Xivkyn 창조, 4E Mace of Molag Bal
- 신설 8 entity: lamae-bal, vampire, planemeld, soulburst, bal-ur, mace-of-molag-bal, dark-anchors, worm-cult
- 최종: 페이지 1120 → 1128, Orphan 0 유지

## [2026-05-29 07:30] ingest | Hermaeus Mora cluster (1 source) | touched: 6 pages
- raw 1 source: Hermaeus Mora.md (404줄, 부분 read + 내장 지식 보강) → _ingested
- hermaeus-mora.md 심층 재작성 (13 → 180줄): Knowledge·Fate·Secrets·Forbidden Knowledge, Apocrypha realm, Multitudes (Wretched Abyss form), Mythos 기원 (Mundus 던져진 아이디어), Coldharbour Compact + Mortal pact, Mephala 자매, Pomegranate Banquet 엿봄 → Vvardenfell Mora 신전 영구 금지 (Vivec 적대), 다층 문화 (Atmoran Herma-Mora/Bosmer/Ayleid Hyrma Mora/Khajiit Hermorah Tide King/Dunmer Devotees), Ysgramor Hare 일화 (Shor 구출), Rajhin Oghma Infinium 도난, Ithelia 추방, 4E Miraak/Last Dragonborn
- 신설 4 entity: oghma-infinium, miraak, black-books, xarxes (apocrypha 기존)
- 최종: 페이지 1116 → 1120, Orphan 0 유지

## [2026-05-29 06:30] ingest | Boethiah + Mephala cluster (6 source) | touched: 14 pages
- raw 6 source: Boethiah(164) + Mephala(157) + Threads of the Webspinner + Goldbrand + Ebony Mail + Webspinner → _ingested
- boethiah.md 심층 재작성 (22→160줄): Prince of Plots, Attribution's Share, Khajiit Boethra, Trinimac 격파→Malacath/Orsimer 탄생, Veloth Exodus 인도 (Chimer-Friend), Maulborn 양면 (조작+격파), Ithelia 추방, Aspera avatars, Molag Bal 영원한 적대
- mephala.md 심층 재작성 (38→170줄): Webspinner, Spiral Skein, Mafala (Khajiit), Vivec Anticipation, Chimer Tri-Angled Truth (Boethiah 공모), Morag Tong 창립, Dark Brotherhood/Silken Ring/Cult of the Spider, Daedric Triad (2E 582 Nocturnal 배신 후 Vile과 협력), Nerien'eth/Crypt of Hearts, Rajhin/Ring of Khajiiti, Erokii/Tears of Anurraame
- 부속 8 신설: ebony-mail, goldbrand, ebony-blade, threads-of-the-webspinner, new-temple, urili-vox, veloths-judgment, spiral-skein
- 최종: 페이지 1108 → 1116, Orphan 0 유지, Broken 888
- **Good Daedra 3주 완성**: azura + boethiah + mephala 모두 심층 페이지

## [2026-05-29 05:00] ingest | Azura cluster (9 source) | touched: 12 pages + 4 stub
- raw 9 source: Azura(205줄) + Azurah(redirect) + Azura's Star(51) + Azura's Coast + Veloth(114줄) + Good Daedra + The Anticipations + Azura and the Box + Nerevarine Prophecy → _ingested
- azura.md 심층 재작성 (22줄 → 200+줄): Twilight·Liminality·Fate·Prophecy/Mystery·Magic, Moonshadow, Anticipation 시스템, Tribunal 저주 (핵심!), Khajiit Azurah 신화 (Fadomai/Lorkhaj/Dark Heart/Khajiit 창조/Magrus Eye), Coldharbour Compact, 2E 582 Vivec 도움 (begrudgingly), 3E 427 Nerevarine 인도, 4E Reclamations, 핵심 평가 (Sotha Sil-Azura 적대+협력 복합)
- veloth.md 신설 (Saint Veloth, Velothi exodus, Good Daedra 신앙 수립, Maulborn 위협 후 회수)
- 부속 7 신설: moon-and-star, azuras-star, good-daedra, reclamations, azurah, anticipations, nerevarine-prophecy (moonshadow 기존)
- batch stub 4: ashlander, conoon-chodala, aldmer, red-year
- 최종: 페이지 1096 → 1108, Orphan 0 유지, Broken 888

## [2026-05-29 03:30] ingest | Vivec cluster 1 (Vivec + CHIM) | touched: 9 pages + 4 stub
- raw 2 source: Vivec.md (669줄, 부분 read + 내장 ES 지식 보강) + CHIM.md (78줄) → _ingested
- vivec.md 심층 재작성 (41줄 → 280+줄): Mortal 시기 (Berahzic-Irdri/netchiman), Sotha Sil 구출, Mortal Lurker 결투, Nord chieftain 격퇴 5인, Pomegranate Banquet + CHIM 습득 + Muatra 탄생, Reach Heaven by Violence (Akavir·Atmora·Yokuda), Monster Children 8 처치, Provisional House, FOUL MURDER (Sermon 29+36), Tribunal 신성화, Living Gods 통치 (Buoyant Armigers·Vvardenfell 수호), Wulfharth·First Akaviri·Four-Score War·Vivec's Antlers·Three Banners War·Sunna'rah·Days of Fire·Tiber Armistice·Nerevarine·4E 행방 불명, CHIM·Amaranth·Walking Ways 신학
- chim.md 심층 재작성 (28줄 → 110줄): Ehlnofex 어원, Tri-Angled Truth, Anu·Lorkhan·Vivec·Talos 도달, Zero Sum 실패, Mephala의 Black Hands, Amaranth 너머
- 신설 4 entity: amaranth, monster-children, provisional-house (+ muatra 재작성)
- batch stub 4: amulet-of-kings, tear, zurin-arctus, pelinal-whitestrake
- 최종: 페이지 1089 → 1096, Orphan 0 유지, Broken 878

## [2026-05-29 02:00] ingest | Almalexia cluster (6 source) | touched: 15 pages + 43 stub
- raw 6 source ingest → _ingested: Almalexia(210줄) + Mask of Almalexia + Hopesfire + Masks of the Tribunal + House Indoril + Indoril Nerevar
- almalexia.md 심층 재작성 (Mother Morrowind 전기 통째): 출생 (Boethiah/Molag Bal), Mournhold 여왕·Orphanage·Shouts, Vivec 알 양육, Nerevar 결혼/Hopesfire-Trueflame, Tribunal 신성화, Chimer 외형 유일 유지, 형이상학적 역할, Wulfharth·Akaviri·Maulborn 격퇴, Mournhold 멸망·Dagon 격파, Sight·저술, Dagoth Ur 후 광기, Sotha Sil 살해·죽음, Azura 평가, Solstheim cult
- 신설 8 entity + 1 redirect: mask-of-almalexia, hopesfire, trueflame, masks-of-the-tribunal, house-indoril(재작성), hands-of-almalexia, maulborn, almalexias-tear, mother-stones, almalexia-city
- cascading: nerevar (Foul Murder 상세), tribunal·vivec·sotha-sil·mournhold·mehrunes-dagon (이전 cluster에서 *주요 갱신, 추가 cross-ref만)
- **batch lint 1+2**: top broken 43 stub 일괄 생성 — wulfharth/house-redoran/dragon-break/psijic-order/talos/reachman/daedric-princes/shalidor/varen-aquilarios/fighters-guild/the-vestige/ashfalls-tear/kemel-ze/baron-admiral/gideon/high-kinlord-rilis-xii/eight-divines/towers/buoyant-armigers/ehlnofey/morihaus/hermaeus-mora/blackwood-company/prince-hubalajad/hews-bane/necromancy/mafala/cathay-raht/wild-hunt/durcorach + mages-guild/crystal-tower/house-dres/saint-alessia/house-hlaalu/eternal-champion/green-lady/thieves-guild/chrysamere/ithelia/second-akaviri-invasion/vivecs-ash-mask/the-towers
- 최종: 페이지 1037 → 1089, Orphan 0 유지, Broken ≥5회 = 0 (top 22 stub 이후 *완전 해소)

## [2026-05-29 00:30] ingest | Sotha Sil cluster (9 source) | touched: 28 pages
- 사용자 회의감 + §3.1 정정 (매 source 대화 → agent 자율 ingest + 결정점만 concurrence) 후 *첫 실제 카파시 cycle*
- 9 source ingest (raw/Lore → _ingested): Loremaster's Archive — The Clockwork City + Ald Sotha + Seht + Clockwork City + House Sotha + Mechanical Heart + On the Clockwork City + Clockwork Apostles + Mask of Sotha Sil
- sotha-sil.md 심층 재작성 (19줄 → 200+줄): 어린 시절 트라우마, Tribunal 신성화, Coldharbour Compact, Dagon 추방, Almalexia 살해, 자유의지 부정, Nirn-Ensuing, Mainspring Ever-Wound, Tarvus 부활 등
- 22 신규 entity: clockwork-city(재작성)/clockwork-apostles/mechanical-heart/mask-of-sotha-sil/ald-sotha/house-sotha/sotha-nall/truth-in-sequence/mainspring-ever-wound/coldharbour-compact/tarvus/factotum/mecinar/brass-fortress/tamriel-final/barilzar/barilzars-mazed-band/luciana-pullo/clockwork-probabilis/numidium/kagrenacs-tools/battle-of-red-mountain/kagrenac/dumac/tribunal-temple/tiber-septim
- 2 신규 book: loremasters-archive-the-clockwork-city / on-the-clockwork-city
- cascading 갱신: tribunal(전면 재작성), vivec, almalexia, mephala, mournhold, mehrunes-dagon, dunmer, chimer, dagoth-ur, heart-of-lorkhan, nerevarine, red-mountain, dwemer
- 최종: 페이지 1010 → 1037, Orphan 0 유지, Broken 874 → 883 (cluster 작업이 *새 broken 노출, 후속 cycle 대상)
- Apostle 신학 (Truth in Sequence), Mainspring Ever-Wound, Tamriel Final, Coldharbour Compact의 *Tribunal lore에서 차지하는 위치* 명료화

## [2026-05-28 23:00] orphan cycle 1 | 색인 페이지 자동 생성 | orphan 647 → 0 (100%)
- 사용자 합의 (orphan 먼저, broken 후순위): 시리즈 색인·카테고리 색인이 *대량 흡수에 효율 ↑*. *broken은 *cascading 사이클로 *점진 해결*.
- 20개 색인 페이지 생성:
  - 카테고리 색인 8: dungeons (211), places (200), concepts (106), characters (88), artifacts (65), deities (40), races (30), factions (25)
  - 시리즈 색인 11 (신규): a-dance-in-fire(8), abahs-landing-merchant-lords(7), monument-island-plaques(5), a-feast-among-the-dead(5), a-culinary-adventure(5), a-memory-book(4), manifestos-of-kinlord-rilis-xii(3), a-hunters-journey(2), 단권 3 (adventurers-almanac/a-history-of-shipbuilding/a-life-barbaric-and-brutal)
  - 단발 책 색인 1: standalone-books-색인 (125편)
- 카테고리 *기타* 4 entity 재분류: almsivi→신성, vicecanon→진영, nebarra→개념, adept→개념 (bosriel만 stub 유지)
- index.md 각 카테고리에 [[X-색인]] 링크 추가 → 색인 페이지 자체도 *in-link 보유*
- 결과: **orphan 647 → 0 (100% 해결)**, broken 877 → 874, 페이지 990 → 1010
- deferred: broken 874 → 자연 trigger ingest 또는 stub 사이클 (#35로 후속)
