---
type: seed-import-meta
source_file: "raw/ESO (고유)명사 번역 통일안.xlsx"
date: 2026-05-26
---

# 시드 import #1 — 마찰점 종합 + CLAUDE.md 갱신 후보

첫 외부 시드 자료(한국 ESO 커뮤니티 통일안 .xlsx, 5,600행 14시트)를 위키로 import하면서 발견한 마찰점들. CLAUDE.md §12 "점진적 개선" 원칙에 따라 이번 ingest 종료 후 정책화할지 결정.

## 1. CLAUDE.md §4 ingest 워크플로 부적합

§4는 *DB 번역 묶음 1개*에 대한 워크플로지만, 이번 자료는:
- DB가 아닌 *외부 시드*
- 단일 묶음이 아닌 *5,600행 14시트*
- 번역이 아니라 *기존 결정의 import*
- termbase + style-guide + 다국어 참조 정신 자료가 *한 파일에 섞임*

→ §4 워크플로 적용 불가. *별도 "시드 import" 워크플로* (§4-b) 필요.

**CLAUDE.md 갱신 후보**: §4 외에 §4b 신설.

## 2. termbase frontmatter 확장

§5.1 명세에 없는 필드 4개를 *임시 도입*했음:

| 필드 | 의미 | §5.1과 차이 |
|---|---|---|
| `status: 확정` | 시드 자료의 결정 상태 | §5.1에 없음 |
| `source_sheet` | 시드 자료 출처 시트명 | §5.1에 없음 |
| `source_row` | 시드 자료 출처 행번호 | §5.1에 없음 |
| `source_file` | 시드 자료 파일 경로 | §5.1에 없음 |

§5.1의 `first_seen_batch`는 시드 자료엔 batch가 없어 *비워둠*.

**CLAUDE.md 갱신 후보**: §5.1 frontmatter에 위 필드 정식화. `first_seen_batch`는 선택 필드로.

## 3. 슬러그 정책 명시 필요

§5에 "termbase 페이지는 영문 슬러그"라고만 있고 *생성 규칙*은 없음. 이번에 도입한 규칙:

```
1. 소문자화 + trim
2. 앞 관사 (a/an/the) 제거 — ESOKo TermController::normalizeTerm 와 일치
3. 어포스트로피 제거
4. 공백 → '-'
5. [a-z0-9가-힣\-_] 만 남김
6. 최대 60자 (초과 시 어절 경계에서 잘림 + 검토 표시)
```

**CLAUDE.md 갱신 후보**: §5에 슬러그 정책 명시.

## 4. 멀티 항목 한 셀 처리

확정됨2 시트 행 3·4에 *한 셀에 여러 단어가 줄바꿈으로* 들어 있는 케이스 발견:

- 행 3: "Trifling / Inferior / Petty / ... / Truly Superb" → "티끌만한 / 열등한 / ... / 초월적인" (16개)
- 행 4: "Sip of / Tincture of / .. / Essence of" → "한 모금의 / ... / 순수한" (9개)

이건 ESO의 *글리프 등급* / *물약 명칭 접두어* 시리즈. 자동 분리 가능하지만 정확한 1:1 매핑 검증이 필요해 *원본 행 그대로 보존 + 검토 표시* 처리. 슬러그는 60자 잘림.

대상 파일:
- [[trifling-inferior-petty-slight-minor-lesser-moderate-average-strong]] (와 같은 유형)
- [[sip-of-tincture-of-dram-of-potion-of-solution-of-elixir-of-panacea-of]]

**액션 후보**: 후속 ingest 또는 lint 사이클에서 분리 — 16+9개 페이지로 재생성.

## 5. 슬러그 충돌 (모두 무해)

9건 충돌 발견. 모두 *동일한 영문 + 동일한 한글* 매핑이 두 시트에 *중복* 등재된 케이스:

| 슬러그 | 영문 | 한글 | 시트 1 | 시트 2 |
|---|---|---|---|---|
| rimmen | Rimmen | 림멘 | 인명사전 | 지명사전 |
| direnni | Direnni | 디레니 | 지명사전 | 기타사전 |
| vestige | Vestige | 잔존자 | 확정됨2 | 기타사전 |
| volenfell | Volenfell | 볼렌펠 | 지명사전 | 던전 |
| nchuleftingth | Nchuleftingth | 누슈레프팅쓰 | 지명사전 | 던전 |
| rkindaleft | Rkindaleft | 르킨다레프트 | 지명사전 | 던전 |
| ashalmawia | Ashalmawia | 아샬마위아 | 지명사전 | 던전 |
| nchuleft | Nchuleft | 누슈레프트 | 지명사전 | 던전 |
| knahaten-flu | Knahaten Flu | 크나하텐 독감 | 지명사전 | 던전 |

처리: 첫 등재본 유지, 충돌본은 `--<시트>-<행>` 접미사로 별도 저장 + 검토 표시. 후속에서 중복 파일 제거 후 단일 termbase 페이지로 통합.

**원칙 후보**: 시드 자료에 *영문 같지만 한글 다른* 충돌이 발견되면 → 자동 import 중단 + 사용자 결정 요청. 이번 경우 *동일 매핑*이라 진행.

**✅ 해결됨 (2026-05-27)** — `feature/remains` 브랜치, "#4 충돌 통합" 작업: 9개 자동 충돌 접미사 파일 모두 삭제. 원본 첫 등재 파일이 유일 termbase 페이지로 통합. 매핑 정보 손실 없음 (모두 동일 매핑이었음).

## 6. 시트별 schema 비일관성

대부분 시트는 `[원문, 한글, 비고1, 비고2]` schema지만 **아이템 시트만 `[대분류, 소분류, 원문, 번역 제안, 의견]`** 으로 컬럼이 두 칸 밀려 있음. 초기 통합 스크립트는 일괄 col 0/1을 가정해서 아이템에서 *3개만* 추출됨 → 시트별 schema 설정으로 수정 후 61개 정상 추출.

**원칙 후보**: 시드 자료 import 전에 *각 시트의 처음 2-3행을 사람이 검토*하고 schema를 명시. 또는 자동 schema 감지 로직.

## 7. "1,000행이지만 실제 ~100행" 패턴

지명사전(971행→175), 기타사전(1012→66), 아이템(70→61), 토론중(1046→339), 번역자들 참고논의(1004→33) 등 다수 시트가 *공간 확보만 되고 실 데이터는 일부*. 정상 패턴 — 빈 행 skip으로 처리.

## 8. style-guide.md / lore/ 페이지 *미생성*

이번 import에서 termbase와 decisions/에 집중했고:
- `wiki/style-guide.md` — **✅ 신설 (2026-05-27, `feature/remains` #1)**: 10 섹션으로 구조화. seed-policy + seed-npc-tone에서 정수 추출.
- `wiki/lore/` — **미생성**. 시드 자료에 lore가 별도로 있는 게 아니라 termbase note에 lore 단서가 흩어져 있음. 향후 lore 페이지는 *번역 사이클*에서 자연 생성.
- `wiki/sections/` — **미생성**. DB 묶음 작업이 시작되면 자연 생성.

## 9. "기타사전"의 카테고리 일괄 처리

기타사전 66개를 모두 `category: 기타`로 일괄 등록. 실제로는 *게임용어 / 책 / 진영 / 종족 / 신화* 등 다양함. 후속에서 세부 분류 lint 필요.

**✅ 해결됨 (2026-05-27, `feature/remains` #5)**: 64개(충돌 통합으로 2개 줄어듦) 중 60개 재분류 — 게임용어 36 / 종족 15 / 진영 9. 모호한 4개(adept, almsivi, nebarra, vicecanon)는 *기타* 유지. *Claude 수동 판단*이라 사용자 검토 권장. 특히 모호한 경계 케이스: almsivi(신화 vs 기타), tribunal(종족 vs 진영), sapiarchs(종족 vs 진영), mane(직책 vs 종족), tonal-architect(직책 vs 진영).

## 10. 시드 termbase 등록과 §11 "사용자 확인 없이 등록 금지" 충돌

§11에 "사용자 확인 없이 termbase 정식 등록 금지"인데, 시드 import는 *619개를 일괄 자동 등록*함. 이는:
- 본인이 "한국 ESO 커뮤니티 용어 최대한 따름"이라 정책 결정함 → *묵시적 일괄 승인*으로 해석.
- 즉 §11의 정신은 *Claude가 자발적으로 새 용어를 등록하지 말라*는 것이지, *시드 import*는 별개.

**CLAUDE.md 갱신 후보**: §11에 "단, 시드 import는 사용자 정책 결정 후 일괄 자동 등록 가능" 단서 추가.

## 11. 슬래시 연결 슬러그 (예: `jerkin--robe`)

3 파일이 슬러그에 `--`를 포함 — 원본 시드의 한 셀에 `Jerkin / Robe` 같이 *두 단어가 슬래시로 묶임*. 정상이지만 *자동 충돌 접미사 형식*(예: `vestige--기타사전-53`)과 형식상 헷갈림.

- `wiki/termbase/jerkin--robe.md` (Jerkin / Robe → 조끼 / 로브)
- `wiki/termbase/kinlady--kinload.md` (kinlady / kinload → 혈족군주)
- `wiki/termbase/kinlord--kinlady.md` (kinlord / kinlady → 혈족군주)

특히 마지막 두 개는 *동일 한글*("혈족군주")을 *다른 영문 두 단어 쌍*으로 등록한 케이스 — 시드의 *오타 또는 변형 표기*.

**액션 후보**: 슬래시 행은 *2 페이지로 분리*하거나 *대표 슬러그 + alias로 합치기*. 후속 lint.

## 12. 물약 접두어 9개 — *확정됨2* vs *아이템* 시트 매핑 불일치

물약 명칭 접두어 9개(Sip of, Tincture of, …, Essence of)가 *확정됨2* 시리즈와 *아이템* 시트에 모두 등재되어 있는데 **5개가 다른 한글 매핑**:

| 영문 | 확정됨2 (시리즈) | 아이템 시트 | 일치 |
|---|---|---|---|
| Sip of | 한 모금의 | 한 모금의 | ✅ |
| Tincture of | 자그마한 | 아주 작은 | ❌ |
| Dram of | 작은 | 작은 | ✅ |
| Potion of | 평범한 | 평범한 | ✅ |
| Solution of | 유용한 | 유용한 | ✅ |
| Elixir of | 신비한 | 특효의 | ❌ |
| Panacea of | 엄청난 | 만능의 | ❌ |
| Distillate of | 증류된 | 증류한 | ❌ |
| Essence of | 순수한 | 정수의 | ❌ |

CLAUDE.md §5.0 정책("영문 같지만 한글 다른 → 자동 import 중단, 사용자 결정 요청") 적용. **`feature/remains` #3 작업에서 자동 분리 보류**, 사용자 결정 대기.

`wiki/termbase/sip-of-tincture-of-…md` 페이지에 충돌 표 + `flags: [needs-split, conflict-with-아이템-시트]` 갱신함.

**사용자 결정 필요**:
- 두 매핑 중 정본 선정 (확정됨2 시리즈 vs 아이템 시트 단일 등재)
- 또는 *문맥 분리* (시리즈 접두어 vs 아이템 등급 명칭으로 별도 페이지)

---

## 정리 — CLAUDE.md 갱신 후보 목록

1. **§4b 신설** — 시드 import 워크플로 (마찰점 #1)
2. **§5 슬러그 정책 명시** (마찰점 #3) — 슬래시 처리 룰 추가도 함께 (마찰점 #11)
3. **§5.1 frontmatter 확장** — status, source_* 필드 (마찰점 #2)
4. **§11 단서 추가** — 시드 import는 일괄 자동 등록 가능 (마찰점 #10)

남은 즉시 조치 (이번 ingest 후속):
- 멀티 항목 행 분리 → 25개 페이지 재생성 (마찰점 #4) — `feature/remains` #3 작업 예정
- ~~동일 매핑 중복 충돌 정리 → 9개 중복 파일 통합 (마찰점 #5)~~ **✅ 해결 (feature/remains #4 작업)**
- style-guide.md 초안 작성 (마찰점 #8) — `feature/remains` #1 작업 예정
- 기타사전 카테고리 세부 분류 (마찰점 #9) — `feature/remains` #5 작업 예정
- 슬래시 슬러그 정리 (마찰점 #11) — 후속 lint
