# scenes — home-intro

director 규칙(.claude/agents/director.md) · 2026-10-30 · 15초 = 450f @30fps
세 안 모두 뼈대 A를 따른다: 글줄 → 폰 상승 → 화면 안 이동 → (클로즈업) → 밀기 · 덮기 → 어두운 끝.

## 3안 요약

**안 1 · 미션이 주인공 (추천)**
- 화면 문구 글줄 → 01-home 폰 상승 → 미션 카드로 이동 → `mission-card` 클로즈업, 진행 바 채워짐 → 컷 → 버튼으로 밀어 들어가 덮기 → 어두운 바탕에서 칩 단어 교체 → 로고
- 쓰는 것: `01-home.png` · `mission-card.html` · `logo.html`
- 반영: refs 1–14 전부 (14/14 = 100%)

**안 2 · 스킬이 주인공**
- 글줄 → 폰 상승 → 아래 "바로 써먹는 스킬"로 이동 → `skill-card-1` 클로즈업 → 컷 → 스킬 카드로 밀어 들어가 덮기 → 어두운 바탕에서 칩 단어 교체 → 로고
- 쓰는 것: `01-home.png` · `skill-card-1.html` · `logo.html`
- 반영: refs 1–9 · 11–14 (13/14 = 93%, 진행 바 #10 없음)

**안 3 · 폰 하나로만**
- 글줄 → 폰 상승 → 화면 안 이동 → 미션 카드로 밀어 들어가 덮기 → 로고. 클로즈업 · 단어 교체 없음
- 쓰는 것: `01-home.png` · `logo.html`
- 반영: refs 1–7 · 11 · 12 · 14 (10/14 = 71%)

## 고른 안: 안 1 · 미션 (승인 1, 2026-10-30)

f = 30fps 프레임. 합계 450f = 15초. 토큰 값은 motion.md · video.md에서 찾는다.

| # | f | 화면 · 부품 | 움직임 · 카메라 · 전환 · 머무름 | 글자 | 놓는 위치 근거 | refs |
|---|---|---|---|---|---|---|
| 1 | 0–65 | 없음 · `video-bg` | 단어 4개 `motion-enter` × `stagger-9` (0 · 9 · 18 · 27, 끝 33) → `hold-read` 33–59 → `motion-exit` 59–65 | "오늘도 하나씩, 내 실력으로" `video-headline` · `video-text` | 01-home 첫 글줄 문구, 화면 정중앙 한 줄 | 1 2 3 4 |
| 2 | 65–172 | `01-home.png` 폰 프레임 | `camera-rise` 65–110 → `hold-screen` 110–172 + `drift-scale` | 없음 | 폰 프레임 가운데 (video.md 4장) | 5 6 |
| 3 | — | 뺌 (스냅보드 피드백: 폰 확대가 5장과 겹침) | | | | |
| 4 | 172–213 | `mission-card.html` ×2.8 | `cut` 172 → 진행 바 0→50% `duration-15` · `ease-out-cubic` 172–187 → `hold-read` 187–213, 카드 전체 172–213 `drift-scale` | 부품 안 문구 그대로 | 화면 가운데 (video.md 5장 크기) | 8 9 10 |
| 5 | 213–251 | `01-home.png` 폰 프레임 | `cut` 213 (2장 끝 상태) → `camera-push` 213–251: "적용 사례 정리하기" 버튼으로, 끝 크기 = `button-submit` ×2.8 폭 980px | 없음 | 01-home 버튼 자리 (y 972–1060 @2x) · video.md 5장 크기 | 9 11 |
| 6 | 251–267 | `video-end-bg` 면 | `camera-cover` 251–257 → `hold-word` 257–267 | 없음 | 화면 전체 | 12 |
| 7 | 267–370 | `video-end-bg` | 윗줄 `motion-enter` 267–273 · 아랫단어 교체 5f씩: 273 · 283 · 293 · 303 (간격 10 · 10 · 10) → `hold-screen` 308–370 | 윗줄 "오늘도 하나씩," `video-title` · 아랫단어 "AI 실무" → "자동화" → "리서치" → "내 실력으로" `video-headline` · `video-end-text` | 01-home 첫 글줄 · 칩 문구, 화면 정중앙 두 줄 | 13 |
| 8 | 370–450 | `logo.html` logotype white ×2.8 | `cut` 370 → `motion-change` 370–382 → `hold-end` 382–450 | 없음 | 화면 정중앙 (video.md 5장) | 14 |

반영 refs: 1–6 · 8–14 (13/14 = 93%). #7 `camera-move`는 3장과 함께 뺌.

수정 2026-10-30 (스냅보드 피드백): 3장 뺌 · 4장 머무름 `hold-screen` → `hold-read`. 남은 84f는 2장 `hold-screen` · 6장 `hold-word` · 7장 `hold-screen`(마지막 문장 2초)으로 채움.

수정 2026-10-30 (영상 피드백: 5초 · 7초에서 끊김): 2 · 4장 머무름에 `drift-scale` 추가. 원인은 f110–171 · f186–212에서 화면이 완전히 멈춘 것 (프레임 누락 아님).

### 새 후보
- **머무는 동안 드리프트**: 승인됨 2026-10-30 → motion.md 1장 `drift-scale` 1 → 1.02 linear.
- **3장 기울기 풀기**: 승인됨 2026-10-30 → motion.md 1장 `rise-tilt-flat` 0°. 3장을 빼서 이번 영상에서는 쓰지 않음.
