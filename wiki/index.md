---
kind: misc
updated: 2026-05-29
---

# Wiki Index

ESOKoLLMWiki 전체 카탈로그. *flat namespace 마이그레이션 후 *재구축*. CLAUDE.md §3.2 *Query 진입점*.

---

## 한눈 통계 (2026-05-29~06-01 대규모 ingest 사이클 — **1600 페이지 마일스톤 달성**)

| 항목 | 수 | 비고 |
|---|---|---|
| **wiki 페이지 (kind 보유)** | **1600** | 🎯 마일스톤 달성 (entity 1400+ + book + decisions 9 + 기타) |
| Entity 추가 (이번 세션) | +613 | 신학·종족·지역·인물·사건·유물·진영·개념 cascade |
| Book | 200+ | raw → 단일 책/문서 흡수 + 시리즈 색인 |
| Decisions | 9 | wiki/decisions/ |
| raw _ingested (Lore 폴더) | **965** | 13950+ 중 6.9% 처리 (대부분 마이너 item) |
| Broken link (unique) | **689** | 마이그레이션 직후 867 → 추가 stub로 ↓ (-178) |
| Orphan (in-link 0) | **0** | 정책: 새 페이지 100% in-link 보장 + 즉시 wikilink |
| 이번 세션 배치 수 | **57+** | 평균 5-22 페이지/배치, 각 배치당 cascade + commit |
| 이번 세션 git commit | **75+** | 각 클러스터별 1-2 commit, DiPoon author override |

## 이번 세션 (2026-05-29) 핵심 ingest 카테고리

- **신학 / 우주** (60+): Aedric 8 + Daedric 16 (+ Ithelia 17) + Tribunal 3 + Good Daedra 3 + 영역 15 (Apocrypha/Coldharbour/Deadlands/Shivering Isles/Hunting Grounds/Spiral Skein/Quagmire/Soul Cairn/Sovngarde/Moonshadow/Evergloam/Pinnacle Rock/Attribution's Share/Detritus/Maelstrom)
- **종족** (30+): 10 본토 종족 + 9 lost races + Werecreature 5 + Vampire 분류 + Daedric 종족 5 + Reachfolk·Hagraven·Giant·Troll·Goblin
- **지역** (40+): 10 본토 province + 29 도시 (Cyrodiil 9 + Skyrim 9 + Morrowind 6 + 기타) + Akavir 5
- **인물·사건** (50+): Tribunal 3 + 5 Companions + 게임 영웅 (Nerevarine/Hero of Kvatch/Last Dragonborn/Vestige/Eternal Champion) + Mannimarco/Tiber Septim/Mankar Camoran/Martin Septim/Barenziah/Helseth/Pelagius III/Akaviri Potentate 등
- **유물** (20+): Amulet of Kings/Numidium/Mantella/Heart of Lorkhan + Daedric Artifact 13
- **진영** (20+): 9 guild + 3 alliance + 5 House + Tribunal Temple + Imperial Legion + Thalmor + Stormcloak 등
- **개념** (30+): CHIM/Mantling/Walking Ways/Tonal Architecture/Towers/Necromancy/Lycanthropy + Voice 5 + Green Pact/Wild Hunt/Lunar Lattice/Magical Transportation/Calendar 등
- **사건** (15+): Battle of Red Mountain/Oblivion Crisis/Soulburst/Planemeld/Greymarch/Great War/Stormcloak Rebellion/Three Banners War/Akavir 침공/Warp in the West/Knahaten Flu/Argonian Invasion/Battle of Sancre Tor/Middle Dawn 등

---

## 진입점 (어디서 시작할까)

- **새 사관**: 세션 시작 의례 (CLAUDE.md §6) → `log.md` 마지막 5줄 → 본 index
- **lore 질문 (사용자)**: 카테고리 섹션 → 해당 entity 페이지 → cross-ref 따라가기
- **Ingest 사이클 (Claude)**: CLAUDE.md §3.1 → raw/Lore 또는 raw/Online에서 *자연 trigger*로 1 source 선택
- **번역 plugin (Phase 2)**: CLAUDE.md §5 → `term:` + `target_ko:` 필드 보유 entity가 *연동 대상*
- **정책 변경 이력**: [[decisions/2026-05-28-mission-pivot]] (가장 큰 사건)

---

## 카테고리별 (Entity)

> 옵시디언 Dataview 플러그인이 있으면 *동적 조회 가능*. 아래는 *주요 entity만 *수동 큐레이션*.

### 신성 (39)
**전체 목록**: [[deities-색인]]
- [[aedra]] · [[daedra]] — Anu·Padomay 양극의 영적 후예
- [[daedric-princes]] — 16 + α 군주 색인
- [[tribunal]] — Almalexia · Sotha Sil · Vivec
- [[sheogorath]] · [[hircine]] · [[mehrunes-dagon]] · [[boethiah]] · [[azura]] · [[mephala]]
- [[akatosh]] · [[arkay]] · [[stendarr]] · [[talos]]
- [[sithis]] · [[anu]] · [[lorkhan]]
- [[hist]] — Argonian 시조 신
- [[fa-nuit-hen]] — Hidden Knower (demiprince)

### 인물 (88)
**전체 목록**: [[characters-색인]]
- [[vivec]] · [[almalexia]] · [[sotha-sil]] — Tribunal 3주
- [[nerevar]] · [[indoril-nerevar]] — Chimer Hortator
- [[abnur-tharn]] · [[varen-aquilarios]] · [[mannimarco]] — ESO 1막 핵심
- [[ayrenn]] · [[jorunn-the-skald-king]] · [[high-king-emeric]] — 3 동맹 지도자
- [[dagoth-ur]] · [[divayth-fyr]] — Morrowind 영겁
- [[tiber-septim]] · [[talos]] — 제 3제국
- [[zaan-the-scalecaller]] · [[shalidor]]

### 지명 (200)
**전체 목록**: [[places-색인]]
- [[tamriel]] · [[nirn]] · [[mundus]] — 세계
- [[morrowind]] · [[skyrim]] · [[high-rock]] · [[hammerfell]] · [[summerset-isles]] · [[valenwood]] · [[elsweyr]] · [[black-marsh]] · [[cyrodiil]] — 9 지방
- [[vivec-city]] · [[necrom]] · [[mournhold]] · [[sadrith-mora]] — Morrowind 도시
- [[the-reach]] · [[markarth]] · [[whiterun]] · [[windhelm]] — Skyrim
- [[systres]] — High Isle DLC
- [[coldharbour]] — Molag Bal의 영지
- [[adamantine-tower]] · [[red-mountain]] · [[baar-dau]] — 신화 지물

### 진영 (24)
**전체 목록**: [[factions-색인]]
- [[aldmeri-dominion]] · [[ebonheart-pact]] · [[daggerfall-covenant]] — 3 동맹
- [[great-houses]] · [[house-telvanni]] · [[house-hlaalu]] · [[house-redoran]] · [[house-indoril]] · [[house-dres]] — Morrowind 가문
- [[dark-brotherhood]] · [[morag-tong]] · [[thieves-guild]] · [[mages-guild]] · [[fighters-guild]] · [[psijic-order]] — 길드
- [[crowns]] · [[forebears]] — Redguard 분파
- [[dragon-cult]] · [[ordinator]] — 종교 조직

### 종족 (30)
**전체 목록**: [[races-색인]]
- [[altmer]] · [[bosmer]] · [[dunmer]] · [[chimer]] · [[falmer]] · [[ayleid]] · [[dwemer]] — Mer
- [[nord]] · [[breton]] · [[imperial]] · [[redguard]] · [[reachman]] — Man
- [[argonian]] · [[khajiit]] · [[orc]] · [[orsimer]] — 그 외
- [[vampire]] · [[werewolf]] · [[goblin]]

### 사건 (1)
- [[2e-582]] — Three Banners War 시작

### 유물 (65)
**전체 목록**: [[artifacts-색인]]
- [[amulet-of-kings]] · [[heart-of-lorkhan]] · [[chim-el-adabal]]
- [[wrathstone]] · [[chrysamere]] · [[volendrung]]

### 개념 (104)
**전체 목록**: [[concepts-색인]]
- [[chim]] · [[walking-ways]] · [[dragon-break]] · [[towers]] — 형이상학
- [[mantling]] · [[soul-gem]] · [[soul-trap]] · [[white-gold-tower]] — 영혼·tower

### 책 (220)
**단발 책 전체 목록**: [[standalone-books-색인]] (125편 시리즈 없는 책)

**시리즈 색인 (11)**:
- [[36-lessons-of-vivec-시리즈-색인]] (37권)
- [[2920-시리즈-색인]] (12권 = 1년 12달)
- [[a-dance-in-fire-시리즈-색인]] (8권)
- [[abahs-landing-merchant-lords-시리즈-색인]] (7권)
- [[monument-island-plaques-시리즈-색인]] (5권)
- [[a-feast-among-the-dead-시리즈-색인]] (5권)
- [[a-culinary-adventure-시리즈-색인]] (5권)
- [[a-memory-book-시리즈-색인]] (4권)
- [[16-accords-of-madness-시리즈-색인]] (3권)
- [[manifestos-of-kinlord-rilis-xii-시리즈-색인]] (3권)
- [[a-hunters-journey-시리즈-색인]] (2권)
- [[adventurers-almanac-시리즈-색인]] · [[a-history-of-shipbuilding-시리즈-색인]] · [[a-life-barbaric-and-brutal-시리즈-색인]] (각 1권)

### 던전 (211)
**전체 목록**: [[dungeons-색인]]
- ESO 인스턴스 던전·delve. 각 던전 페이지에 입장 조건·boss·loot 정보.

---

## 메타 페이지

- [[index]] (본 페이지)
- [[log]] — 시간순 작업 로그
- [[style-guide]] — 번역 plugin용 톤·규칙 (Phase 2)
- [[decisions/2026-05-28-mission-pivot]] — 미션 재정의 (네임스페이스 폐기)
- [[decisions/2026-05-25-meta-termbase-emergency]] — 위반 사례 회고 (legacy)
- [[decisions/seed-policy-eso-고유명사-xlsx]] — 시드 import 정책
- [[decisions/seed-import]] — 시드 종합 회고
- [[decisions/round-1]] ~ [[decisions/round-5]] — 라운드별 회고 (legacy)

---

## 데이터셋 옵시디언 Dataview 예시

옵시디언 Dataview 플러그인 활성화 시:

````dataview
TABLE category, kind, status
FROM "wiki"
WHERE kind = "entity" AND status = "stub"
SORT category, file.name
````

stub 페이지만 우선 보강할 때 활용.

````dataview
TABLE category, length(file.outlinks) AS out
FROM "wiki"
WHERE kind = "book" AND length(file.outlinks) < 2
SORT file.name
````

cross-ref 부족 책 페이지 식별.

---

## 알려진 문제 (마이그레이션 후)

1. **Orphan 65.4%** — 대부분 책 페이지가 *카테고리 본문에 *링크 안 됨*. 시리즈 색인·카테고리 페이지로 *흡수 필요* (deferred).
2. **Broken link 867** — 주로 책 본문이 언급한 작은 entity 전용 페이지 없음. ≥5회 22종은 *stub 완료*. 나머지는 자연 trigger 대기 또는 다음 cascading 사이클.
3. **Cross-ref 양방향 누락** — A→B 링크 있는데 B에 A backlink 없음. 옵시디언 backlink 패널 또는 Dataview로 해결 가능.
4. **카테고리 "기타" 5종** — `adept`, `almsivi`, `vicecanon`, `nebarra`, `bosriel` — 정확 분류 후속 결정 필요.
