# motion.md

움직임 성격: **경쾌**. 빨리 들어오고, 페이드 없이 컷으로 넘기고, 반복되는 것은 점점 빨라진다.
규칙: 이 문서에 있는 값만 쓴다. 색 · 글자 · 로고 · 장면 순서 · 화면 배치는 여기서 정하지 않는다 (영상마다 비트 시트로).
문서에 없는 숫자가 필요한 움직임은 쓰기 전에 **"새 후보"**로 묻고, 승인되면 이 문서에 추가한다.

출처 (2026-10-30 분석)
- **[R] Remotion 문서** "Apple-Style Device Rise Animation" (remotion.dev/prompts, 1280×720 · 30fps). 문서에 적힌 값을 그대로 옮겼다.
- **[V] 영상** skillry `saadpastadev-347341` (1280×720 · 24.55s · 30fps, `references/saadpastadev-347341.mp4`).
  프레임마다 화면 변화량을 재서 값을 뽑았다. 시점 표기는 `mm:ss.xx`.

단위: **f = 1프레임 @30fps (33.3ms)**. 영상 fps가 바뀌면 ms를 기준으로 다시 계산한다.

---

## 1. Primitives

### 길이 (duration, 6단계)

| 변수 | f | ms | 출처 |
|---|---|---|---|
| `duration-4` | 4 | 133 | [V] 00:05.50 검색창 타이핑, 글자 하나당 4f (00:05.50 · 05.63 · 05.77) |
| `duration-6` | 6 | 200 | [V] 00:00.37 단어 등장 6f, 00:00.80 단어 퇴장 7f |
| `duration-12` | 12 | 400 | [V] 00:06.20 검색창 → 알약 변형 12f, 00:14.60 알림 내려오기 11f |
| `duration-15` | 15 | 500 | [V] 00:06.67 점 → 선 그래프 그려짐 15f |
| `duration-38` | 38 | 1267 | [V] 00:09.23 화면 이동 38f, 00:12.57 밀어 들어가기 37f, 00:15.10 밀어 들어가기 32f + 검은 면 덮기 6f |
| `duration-45` | 45 | 1500 | [R] "Total animation duration: 1.5 seconds" |

### 곡선 (easing)

| 변수 | cubic-bezier | Remotion | 출처 |
|---|---|---|---|
| `ease-out-cubic` | `0.33, 1, 0.68, 1` | `Easing.out(Easing.cubic)` | [R] "Use … Easing.out(Easing.cubic) for all animations" · [V] 00:00.37 단어 등장: 변화량이 첫 프레임에 가장 크고 줄어듦 |
| `ease-in-cubic` | `0.32, 0, 0.67, 0` | `Easing.in(Easing.cubic)` | [V] 00:00.80 단어 퇴장 · 00:16.17 검은 면 덮기: 변화량 22→47로 커짐 |
| `linear` | `0, 0, 1, 1` | `Easing.linear` | [V] 00:12.57 밀어 들어가기: 37f 동안 변화량 5~8로 거의 일정 · 00:15.10–00:16.13 변화량 3~9 (2026-10-30 정정, 처음엔 `ease-in-cubic`으로 잘못 봄) |
| `ease-in-out-cubic` | `0.65, 0, 0.35, 1` | `Easing.inOut(Easing.cubic)` | [V] 00:09.23 화면 이동: 13f째(38f 중)에 가장 빠름 |
| `step` | 없음 (곡선 없이 바로 바뀜) | 없음 | [V] 00:05.50 타이핑 · 00:11.50 숫자 바뀜 · 00:12.50 컷 |

cubic-bezier 값은 같은 이름 곡선의 표준 근사값이다. Remotion에서는 오른쪽 열의 함수를 쓴다.

### 간격 · 크기 (기타 숫자)

| 변수 | 값 | 출처 |
|---|---|---|
| `stagger-9` | 9f (300ms) | [R] "staggered timing (0.3s apart)" |
| `rise-offset` | 프레임 높이의 0.56 (1280×720에서 400px) | [R] "translateY: 400px down" |
| `rise-tilt-from` · `rise-tilt-to` | 35° · 8° (rotateX) | [R] "starts at ~35 degrees and settles to ~8 degrees" |
| `rise-scale-from` | 0.8 → 1.0 | [R] "Scale from 0.8 to 1.0" |
| `drift-scale` | 1 → 1.02, `linear`, 머무는 시간 내내 | 새 후보 승인 2026-10-30 (home-intro): 머무는 동안 화면이 멈추지 않게. 레퍼런스 측정값 아님, 제안값 |
| `rise-tilt-flat` | 0° (rotateX) | 새 후보 승인 2026-10-30 (home-intro): 기운 폰에서 평평한 부품으로 바꿔 끼우기 전 `camera-move` 동안 풂 |

---

## 2. Semantic (5개)

Primitive를 직접 쓰지 않고 이 이름으로 쓴다.

| 변수 | 길이 | 곡선 | 쓰는 곳 | 출처 |
|---|---|---|---|---|
| `motion-enter` | `duration-6` | `ease-out-cubic` | 글줄 · 카드 · 배지가 나타날 때 | [V] 00:00.37 글줄 등장 6f |
| `motion-exit` | `duration-6` | `ease-in-cubic` | 사라질 때. 다음 것이 바로 이어지면 `step`(컷) | [V] 00:00.80 글줄 퇴장 7f → 6f로 맞춤 |
| `motion-change` | `duration-12` | `ease-out-cubic` | 같은 부품의 상태 · 모양이 바뀔 때 | [V] 00:06.20 검색창 → 알약 12f |
| `motion-rise` | `duration-45` | `ease-out-cubic` | 화면(기기)이 아래에서 올라와 자리 잡을 때 | [R] 1.5s · ease-out cubic |
| `motion-camera` | `duration-38` | `ease-in-out-cubic` | 화면 안에서 시점이 옮겨갈 때 (5장) | [V] 00:09.23 화면 이동 38f |

- 여러 개가 차례로 들어올 때: `motion-enter`를 `stagger-9` 간격으로. [R] 알림 카드 0.3s 간격
- 컷: 0f, 페이드 없음. [V] 00:12.50 · 00:13.87 모두 한 프레임에 바뀜. 밀기 끝은 컷 대신 `camera-cover` (5장)

---

## 3. Pattern

### src/parts

| 부품 | 움직임 | 토큰 | 출처 |
|---|---|---|---|
| `button-submit.html` | 문구 바뀜 (`data-state` 4개) | 글자만 `step`으로 바꾸고 버튼 틀은 그대로 | [V] 00:11.50 금액 숫자 한 프레임에 바뀜 |
| `button-submit.html` | 누름 · 제출 | `motion-change` | [V] 00:12.57 밀어서 확인 버튼 37f 중 반응 |
| `badge-approved.html` | 나타남 | `motion-enter` | [V] 00:14.00 체크 표시 등장 |
| `skill-card-1~3.html` | 목록으로 들어옴 | `motion-enter` × `stagger-9` | [R] 0.3s 간격 · [V] 00:16.57 목록 반복 |
| `asset-card.html` | 상태 바뀜 (`data-state` 4개) | `motion-change` | [V] 00:06.20 모양 변형 12f |
| `mission-card.html` | 진행 바 채워짐 | `duration-15` · `ease-out-cubic` | [V] 00:06.67 선 그래프 그려짐 15f |
| `stat-card.html` | 숫자 바뀜 | `step` | [V] 00:11.50 숫자 한 프레임에 바뀜 |
| `logo.html` · `brand-icon.html` | 마지막에 나타남 | `motion-change` (12f) | [V] 00:21.90 마지막 글줄 등장 11f |

### src/screens

| 화면 | 움직임 | 토큰 | 출처 |
|---|---|---|---|
| 첫 등장 (모든 화면 공통) | 아래에서 올라오며 기울기 · 크기 풀림 | `motion-rise` + 5장 `camera-rise` | [R] |
| `01-home` · `02-skills` 검색 · 칩 | 검색어 타이핑 | 글자당 `duration-4` · `step` | [V] 00:05.50 |
| `03-mission` 결과물 제출 | 제출 버튼 → 다음 상태 | `motion-change` 뒤 `step` 컷 | [V] 00:12.57 → 00:13.87 |
| `04-approved` | 배지 · 피드백 | `motion-enter` × `stagger-9` | [V] 00:14.00 · [R] 0.3s |
| `05-assets` | 수익 카드 → 자산 목록 | 카드 `step`, 목록 `motion-enter` × `stagger-9` | [V] 00:11.50 · [R] |
| 화면 → 화면 | 같은 기기 안이면 `motion-camera`, 다른 장면이면 컷 | | [V] 00:09.23 · 00:12.50 |

---

## 4. 머무는 시간

움직임이 끝난 뒤 다음 움직임까지 멈춰 있는 시간.

| 변수 | f | 쓰는 곳 | 출처 |
|---|---|---|---|
| `hold-word` | 10 | 짧은 글줄 하나 | [V] 00:00.47–00:00.80 두 단어 글줄 |
| `hold-read` | 26 | 한 줄 문장을 읽는 시간 | [V] 00:21.03–00:21.90 마지막 문장 |
| `hold-screen` | 62 | 화면 하나를 보여주는 시간 | [V] 00:07.17–00:09.23 그래프 화면 |
| `hold-end` | 68 | 영상 마지막 | [V] 00:22.27–00:24.55 마지막 글줄 |

- 반복 목록은 점점 빨라진다: 항목 간격 10f에서 시작해 7f까지 줄인다. 한 항목이 바뀌는 데 5f. [V] 00:16.57–00:20.93
- 머무는 동안에도 화면이 완전히 멈추지 않는다: 그래프가 작게 계속 움직인다. [V] 00:07.20–00:09.03 → 화면 · 부품이 머무는 동안 `drift-scale`

---

## 5. 카메라

| 변수 | 움직임 | 길이 · 곡선 | 출처 |
|---|---|---|---|
| `camera-rise` | `rise-offset`만큼 아래에서 올라옴, rotateX `rise-tilt-from` → `rise-tilt-to`, scale `rise-scale-from` | `motion-rise` | [R] |
| `camera-move` | 같은 화면 안에서 다른 부분으로 옮겨감 | `motion-camera` | [V] 00:09.23 38f |
| `camera-push` | 한 부품으로 일정한 속도로 밀어 들어감 | `duration-38` · `linear` | [V] 00:12.57 37f (38f로 맞춤) · 2026-10-30 정정 |
| `camera-cover` | 밀기 끝에 어두운 면이 덮으며 넘어감 (색은 video.md) | `duration-6` · `ease-in-cubic` | [V] 00:16.17–00:16.33 6f. 처음엔 밀기의 가속으로 잘못 봄 |
| `cut` | 바로 바뀜 | 0f · `step` | [V] 00:12.50 · 00:13.87 |

`camera-rise` 구현 [R]:
- `transformOrigin: "center bottom"`
- 순서: `translateX(-50%)` → `translateY()` → `rotateX()` → `scale()`
- `perspective` 값은 문서에 없음 → 새 후보로 물을 것.
- 페이드(투명도로 넘기기)는 쓰지 않는다. [V] 장면 전환은 컷, 밀기 끝만 `camera-cover`
