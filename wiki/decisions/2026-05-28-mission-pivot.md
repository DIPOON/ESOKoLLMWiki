---
date: 2026-05-28
type: 결정 (mission pivot)
status: 채택 (사용자 결정)
---

# 2026-05-28 미션 재정의 — ES 전문가 wiki

## 사용자 결정 (인용)

> "결국 LLM wiki 는 에이전트 AI 에게 엘더 스크롤 전문가가 되도록 만들어야 한다고 생각해요. 번역 API 를 붙여서 쓰고 이거는 후순위 문제이구요."

> "termbase 가 엘더 스크롤 온라인의 고유어 모음 같은 것이면 lore 에서 직접 참조를 하는 것이 맞지 않나"

## 변경 전 미션 (CLAUDE.md §0, 2026-05-25 작성)

- ESOKoLLMWiki = **ESOKo 프로젝트의 *큐레이션 레이어***
- ESOKo의 *MySQL DB와 *같은 정본*. Laravel API로 *DB 동기화*
- wiki = *번역 결정의 *뇌*
- **termbase/ namespace** = *DB `terms` 테이블의 *거울*

## 변경 후 미션

- ESOKoLLMWiki = **Elder Scrolls Online *지식 위키***
- *카파시 LLM Wiki 패턴* 그대로
- 목적:
  1. **agent (Claude)가 *ES 전문가가 *되도록 *증분 구축***
  2. ES 게임 시 *반려·자문 AI*
  3. (후순위) 번역 API plugin: frontmatter `term:` 필드로 *DB sync*
- **wiki/ flat directory** — namespace 분리 X. *모두 wiki/<slug>.md*

## 변경의 *근거*

1. **Phase 2 미진입**: ESOKo API + DB 테이블 *전부 미구현, 0회 사용*. *미실현 미래를 위해 *현 wiki 왜곡 가치 X*
2. **termbase namespace의 *기능적 가치 0*** (Phase 1):
   - termbase 696개 중 *lore 페이지에서 *cross-ref 4개*만
   - lore에서 termbase 인용 시 *[[X|한글]] 번거로움*
   - *Tamriel·Nirn·Adamantine Tower·Vivec City* 등이 *termbase·lore 어느 쪽에 둘지 *경계 모호*
3. **카파시 정신** = *flat wiki* (단일 directory). *namespace 분기 자체가 *원래 없음*

## 영향 범위

- **CLAUDE.md 전면 재작성**: §0 미션, §1 구조, §2 API, §4 워크플로, §5 페이지 규약, §7-§11 — 거의 *모두 갱신*. Phase Marker 폐기. ESOKo 섹션 *plugin 후순위로 강등*.
- **디렉토리 마이그레이션**: 696 termbase + 270 lore → wiki/<slug>.md flat. wiki/decisions/만 유지 (메타-결정 분리).
- **위키링크 일괄 교체**: `[[X]]`, `[[X]]` → `[[X]]`. 수천 개 교체 예상.
- **frontmatter 통일**: `kind: entity | book | synthesis | decision | misc` 필드 도입. *현재 산발적 *category 22종 → 통합*.
- **번역 도메인 후순위**: ESOKo API, claude_batches, terms 테이블 매핑 등은 *향후 *plugin*으로 *분리 처리*. 본 wiki는 그것 없이 *자립*.

## 변경의 *진짜 의미*

이 위키는 *번역 도구의 *부속*이 아니라 **그 자체로 *Elder Scrolls 지식 그래프***. 번역은 *그 위에 올라가는 *application*. *카파시 정신*의 *모든 의미*가 *이 결정으로 비로소 *살아남*.

## 이어지는 작업

1. CLAUDE.md 전면 재작성 (이 결정 기반)
2. termbase → wiki flat 마이그레이션
3. 위키링크 일괄 교체
4. broken link cascading 보강
5. orphan 정리
6. cross-ref 양방향 회복
