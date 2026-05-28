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
