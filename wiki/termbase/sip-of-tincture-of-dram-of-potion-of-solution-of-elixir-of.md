---
term: "Sip of (외 8개)"
target_ko: "한 모금의 (외 8개)"
target_de:
target_ja:
aliases: [물약 접두어]
category: 게임용어
status: 확정
flags: [needs-split, conflict-with-아이템-시트]
source_sheet: 확정됨2
source_row: 4
source_file: "raw/ESO (고유)명사 번역 통일안.xlsx"
---

# 물약 명칭 접두어 시리즈 (9개) — 분리 보류 (충돌 발견)

⚠ **분리 보류 (2026-05-27, `feature/remains` #3)**. 9개 영문 모두 *아이템* 시트에도 단독 등재되어 있는데, **5개가 다른 한글 매핑**. CLAUDE.md §5.0 "영문 같지만 한글 다른 → 자동 import 중단, 사용자 결정 요청" 정책 적용. ([[seed-import]] 마찰점 #12)

## 채택 근거 (시드 자료 원본 description, 확정됨2 시트)
- 연금액 방울: 체력
- 연금액 팅크처: 체력
- 연금액 컵: 체력
- 연금액 포션: 체력
- 연금액 용매: 체력
- 연금액 영약: 체력
- 연금액 파나케이아: 체력
- 연금액 증류수: 체력
- 연금액 정수: 체력
- (구버전)

## 충돌 매핑 (확정됨2 시리즈 vs 아이템 시트 기존 termbase)

| 영문 | 확정됨2 (시리즈) | 아이템 시트 (기존 페이지) | 일치 |
|---|---|---|---|
| Sip of | 한 모금의 | 한 모금의 ([[sip-of]]) | ✅ |
| Tincture of | 자그마한 | 아주 작은 ([[tincture-of]]) | ❌ |
| Dram of | 작은 | 작은 ([[dram-of]]) | ✅ |
| Potion of | 평범한 | 평범한 ([[potion-of]]) | ✅ |
| Solution of | 유용한 | 유용한 ([[solution-of]]) | ✅ |
| Elixir of | 신비한 | 특효의 ([[elixir-of]]) | ❌ |
| Panacea of | 엄청난 | 만능의 ([[panacea-of]]) | ❌ |
| Distillate of | 증류된 | 증류한 ([[distillate-of]]) | ❌ |
| Essence of | 순수한 | 정수의 ([[essence-of]]) | ❌ |

**불일치 5건 — 사용자 결정 필요**:
- 두 매핑 중 어느 게 정본? (또는 *문맥 다름* — 시리즈 접두어 vs 아이템 등급 명칭이라 별도 페이지 유지?)
- 결정 후: 5개 시리즈 항목 신설(`tincture-of-series.md` 같은 별도 슬러그?) 또는 기존 페이지 갱신.

## 출처
- `raw/ESO (고유)명사 번역 통일안.xlsx` — 시트 *확정됨2*, 행 4 (한 셀에 9개 묶임)
- 한국 ESO 커뮤니티 합의
