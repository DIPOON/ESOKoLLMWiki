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
