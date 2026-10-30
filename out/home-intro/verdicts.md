# verdicts — home-intro

critic 규칙(.claude/agents/critic.md). 한 줄씩 덧붙인다.

- 2026-10-30 · 스냅보드 · 통과 — G1 docs에 없는 숫자 0 · G2 화면에 없는 UI 0 · G3 반영 14/14 (100%) · G4 근거 8/8
- 2026-10-30 · 스냅보드 v2 (사람 피드백: 3장 뺌 · 4장 hold-read) · 통과 — G1 0 · G2 0 · G3 반영 13/14 (93%) · G4 근거 7/7
- 2026-10-30 · 영상 · 통과 — G1 0 · G2 0 · G3 13/14 · G4 7/7 · video.mp4 1920×1080 · 30fps · 450f · 15.000s (장면표와 같음), 프레임 8 · 45 · 150 · 198 · 230 · 249 · 254 · 345 · 420 디코딩해 스냅보드 v2와 대조
- 2026-10-30 · 영상 v2 (사람 피드백: 5초 · 7초 끊김 → `drift-scale`) · 통과 — G1 0 (`drift-scale` 승인 후 motion.md 1장에 적음) · G2 0 · G3 13/14 · G4 7/7 · 450f · 15.000s, f110–212 멈춘 프레임 0 (프레임 변화량 0.07–0.17)

<details><summary>2026-10-30 스냅보드 센 내용</summary>

- G1: 길이 · 곡선은 모두 토큰(6 · 9 · 15 · 38 · 45f, power2 = cubic, linear). 확대 ×2.4987 · ×2.75는 video.md 5장 폭 980에서, 이동량 1.6 · −100.6 · −1.1px는 01-home 위치에서 나온 값(G4). 마스크 이동 95 · 90 · 53px는 video.md 3 · 5장 줄 높이 · 로고 높이. 기울기 0°는 승인된 `rise-tilt-flat`. 색은 모두 design.md.
- G2: 보이는 UI = `01-home.png` · `mission-card.html` · `logo.html` logotype-white. 글줄 · 단어는 01-home 문구 · 칩.
- G3: refs 1–14 모두 확인 (3 · 13은 정지 화면 대신 코드 타이밍으로 확인).
- 참고 (hyperframes check, 오류 0): 대비 4.48:1은 부품 원본 `color-text-muted`, 짧은 단어 표시는 레퍼런스 A 리듬(motion.md 4장). 게이트 대상 아님.
</details>
