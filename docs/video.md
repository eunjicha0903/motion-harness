# video.md

영상 룩. **16:9 · 1920×1080 · 30fps**. 움직임 값은 [motion.md](motion.md)에 있다.
규칙: 색 · 폰트는 [design.md](design.md)에서만 가져온다. 영상 글자 크기 = Figma 값 × **2.8** (모션용 텍스트 배율), 반올림해서 정수 px.
장면 순서 · 흐름 · 구성은 여기서 정하지 않는다 (레퍼런스와 비트 시트가 정함).
결정 (2026-10-30): 배경 **밝은** · 헤드라인 **단정하게** · 엔드 카드 **어두운**.

---

## 1. 텍스트 최소 크기

| 변수 | 값 | 출처 |
|---|---|---|
| `video-text-min` | **31px** | `Text/eyebrow` 11px × 2.8 = 30.8 |

- 화면에 찍힌 크기 기준이다. 31px보다 작은 글자는 읽히는 글자로 쓰지 않는다.
- 예외: 폰 프레임(4장) 안의 화면 이미지. 화면 전체를 보여주는 용도라서 그 안의 글자는 읽히지 않아도 된다.
  그 안의 글자를 읽혀야 하면 화면 이미지를 키우지 말고 5장 parts를 ×2.8로 따로 띄운다.

---

## 2. 배경

| 변수 | hex | design.md | 쓰는 곳 |
|---|---|---|---|
| `video-bg` | `#ffffff` | `color-bg` | 본편 바탕 (밝은) |
| `video-surface` | `#f7f7f8` | `color-surface` | 바탕 위 면 · 판 |
| `video-end-bg` | `#18191b` | `color-text` | 엔드 카드 바탕 (어두운) · motion.md `camera-cover`의 덮는 면 |

- 그라데이션 · 패턴 · 사진 바탕은 쓰지 않는다. design.md에 없는 색이다.
- 일러스트 색(`color-illustration-*`)은 parts와 캐릭터 안에서만 쓰고 바탕으로 쓰지 않는다.

---

## 3. 글자

폰트: **Pretendard** 400 · 600 · 700, 로컬 파일 `src/assets/fonts/` (design.md 3장 A). 첫 프레임 전에 `document.fonts.ready`를 기다린다.
자간 0%. 크기 · 행간 모두 Figma × 2.8.

| 변수 | Figma 스타일 | 굵기 | 크기 px | 행간 px | 쓰는 곳 |
|---|---|---|---|---|---|
| `video-headline` | `Text/display` 28/34 | 700 | **78** | 95 | 헤드라인. 이보다 크게 쓰지 않는다 (단정하게) |
| `video-title` | `Text/title` 24/32 | 600 | 67 | 90 | 헤드라인 다음 줄 · 짧은 문장 |
| `video-body` | `Text/body` 15/24 | 400 | 42 | 67 | 설명 문장 |
| `video-label` | `Text/label` 14/20 | 600 | 39 | 56 | 짧은 이름 · 숫자 옆 단위 |
| `video-caption` | `Text/caption` 12/16 | 400 | 34 | 45 | 출처 · 보조 문구 |
| `video-eyebrow` | `Text/eyebrow` 11/16 | 600 | 31 | 45 | 헤드라인 위 작은 머리말 (= 최소 크기) |

글자 색

| 변수 | hex | design.md | 쓰는 곳 |
|---|---|---|---|
| `video-text` | `#18191b` | `color-text` | 밝은 바탕 위 기본 글자 |
| `video-muted` | `#75777c` | `color-text-muted` | 보조 글자 |
| `video-accent` | `#3759de` | `color-primary` | 강조 단어 하나 |
| `video-end-text` | `#ffffff` | `color-on-primary` | 엔드 카드 위 글자 |

- 한 장면에 강조 색은 `video-accent` 하나만. 굵기는 400 · 600 · 700 세 개뿐이다.
- 나머지 Figma 스타일(`compact-title` 62 · `section` 56 · `heading` 50 · `list-title` 42)은 parts 안에서만 쓰인다.

---

## 4. 폰 프레임

`src/screens/*.png` (780×1688 = 390×844 @2x)를 감싸는 기기 틀. 비율은 Remotion 문서 [R] "Apple-Style Device Rise Animation" (720p 기준)을 1080p로 ×1.5 옮겼다.

| 변수 | 값 | 출처 |
|---|---|---|
| `phone-height` | 975px (프레임 높이의 0.9) | [R] 기기 높이 650px / 720 |
| `phone-bezel` | 15px | [R] 바깥 모서리 45 − 안쪽 35 = 10px × 1.5 |
| `phone-screen` | 437 × 945px (390×844 × 1.12) | `phone-height` − 위아래 `phone-bezel` |
| `phone-width` | 467px | `phone-screen` 폭 + 양옆 `phone-bezel` |
| `phone-radius` · `phone-screen-radius` | 68px · 53px | [R] 45px · 35px × 1.5 |
| `phone-color` | `#18191b` | design.md `color-text` ([R]의 #1a1a1a 대신) |
| `phone-shadow` | 0 · 22 · 67 · 0, `#0000001F` | design.md `Shadow/lg` × 2.8 |

- 화면 이미지는 자르거나 늘리지 않고 `phone-screen`에 꽉 맞춘다 (비율이 같다).
- 상태 표시줄 · 다이내믹 아일랜드는 그리지 않는다. 화면 이미지에 있는 그대로 쓴다.
- 반사광 · 유리 질감 · 실제 기종 모양은 넣지 않는다.
- 폰 안으로 밀어 들어갈 때(motion.md `camera-push`)는 **일정한 속도(`linear`)**로 움직이고, 끝에서 `video-end-bg` 면이 덮는다(`camera-cover`). 밀기 자체를 점점 빠르게(ease-in) 하지 않는다. 2026-10-30 정정
- 밀기 중에도 폰 프레임의 `phone-bezel` · `phone-radius` · `phone-shadow`는 같은 배율로 함께 커진다. 테두리만 따로 두지 않는다.

---

## 5. parts

`src/parts/*.html`을 그대로 ×2.8로 키워서 쓴다. px 값을 고쳐 쓰지 않는다.
- 방법: 감싸는 요소에 `transform: scale(2.8)` · `transform-origin: top left`. 이미지로 뽑을 때는 deviceScaleFactor 2.8로 렌더링해서 흐려지지 않게 한다.
- 부품 안의 글자 · 모서리 · 그림자도 함께 ×2.8이 된다. 가장 작은 글자(`Text/caption` 12)는 34px가 되어 `video-text-min`을 넘는다.
- `_check/*.png`는 확인용이다. 영상에 넣지 않는다.

| 부품 | Figma 크기 | 영상 크기 (×2.8) | 비고 |
|---|---|---|---|
| `asset-card.html` | 350×74 | 980×207 | `data-state` 4개 |
| `badge-approved.html` | 108×32 | 302×90 | |
| `brand-icon.html` | 98×98 | 274×274 | |
| `button-submit.html` | 350×44 | 980×123 | `data-state` 4개 |
| `logo.html` logotype · symbol | 149×19 · 100×100 | 417×53 · 280×280 | 밝은 바탕은 black, `video-end-bg` 위는 white |
| `mission-card.html` | 350×253 | 980×708 | |
| `skill-card-1~3.html` | 350×88 | 980×246 | |
| `stat-card.html` | 350×101 | 980×283 | |

- 부품 바탕은 부품 자체의 색을 쓴다. `video-bg` 위에서 부품 테두리(`color-border`)와 그림자가 그대로 보이게 둔다.
- 엔드 카드에는 `logo.html` white 변형과 `video-end-text`만 쓴다.
