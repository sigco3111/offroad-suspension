# 🏔️ offroad-suspension

> HTML5 Canvas + Matter.js 기반 2D 오프로드 자동차 서스펜션 시뮬레이터

울퉁불퉁한 절벽 지형을 달리는 2D 자동차. **차체-바퀴 사이 스프링/댐퍼(Shock Absorber) Constraint 물리**로 지형 충격을 흡수하고, 가속·제동 시 관성 모멘텀이 자연스럽게 반영되는 드라이빙 시뮬레이터입니다. R 키로 즉시 리셋, 화살표/WASD로 직관적 조작, 카메라가 차량을 부드럽게 추적합니다.

[🇰🇷 한국어 (기본)](#) · [🇺🇸 English](./README.en.md)

---

## 🎬 라이브 데모

> **👉 [https://sigco3111.github.io/offroad-suspension/](https://sigco3111.github.io/offroad-suspension/)** — 브라우저에서 바로 실행 (60fps, Matter.js CDN)

| | |
|---|---|
| ![Demo](https://img.shields.io/badge/Live-Demo-222222?style=for-the-badge&logo=githubpages&logoColor=white) | [![Repo](https://img.shields.io/badge/GitHub-sigco3111%2Foffroad--suspension-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/sigco3111/offroad-suspension) |
| ![Status](https://img.shields.io/badge/Status-Live-22C55E?style=flat-square) | ![Stack](https://img.shields.io/badge/Stack-Matter.js-F7DF1E?style=flat-square&logo=javascript&logoColor=black) |
| ![License](https://img.shields.io/badge/License-MIT-F1C40F?style=flat-square) | ![Deps](https://img.shields.io/badge/Dependencies-2_CDN-9CA3AF?style=flat-square) |

### 🎮 빠른 사용법
1. 위 데모 링크 클릭 → 브라우저에서 페이지 열기
2. **→ / D** — 가속 (전진)
3. **← / A** — 브레이크 / 후진
4. **스페이스바** — 핸드브레이크 (마찰력 ↑)
5. **R 키** — 차량 + 지형 리셋
6. **C 키** — 카메라 추적 모드 토글

---

## 🤖 생성 정보

이 프로젝트의 코드는 아래 모델과 프롬프트를 이용해 **자동으로 생성**되었습니다.

| 항목 | 값 |
|---|---|
| **모델** | MiniMax-M3 |
| **실행 환경** | OpenCode CLI |
| **저장소** | [`sigco3111/offroad-suspension`](https://github.com/sigco3111/offroad-suspension) |
| **라이선스** | MIT |
| **의존성** | 2개 (matter-js@0.20.0, poly-decomp@0.3.0 — 모두 jsDelivr CDN) |

### 📝 사용된 프롬프트 (원문)

```
2D 오프로드 자동차가 울퉁불퉁한 절벽 지형을 달리는 시뮬레이터를 만들어줘.
차체(Chassis)와 두 개의 바퀴(Wheels) 사이에 스프링/댐퍼(Shock Absorber)
Constraint를 추가해서 진짜 자동차처럼 지형 충격을 흡수하는 느낌이 나야 해.
화살표 키 또는 WASD로 가속/브레이크/후진을 할 수 있고, 스페이스바로
핸드브레이크가 걸려서 마찰력이 높아져야 해. R 키로 차량과 지형이 리셋되고,
C 키로 카메라 추적 모드를 토글할 수 있어야 해. 차량에 카메라가 따라가도록
해서 큰 지형에서도 차가 화면 중앙에 유지되도록 해줘.
Implementation Advice: Use Matter.js (matter-js@0.20.0) Bodies.fromVertices
for terrain polyline, Constraint for spring/damper between chassis and wheels.
Tune stiffness (0.05-0.15) and damping (0.1-0.3) for realistic oscillation.
Apply torque to wheels for drive, use Body.setAngularVelocity for spin.
모든 의존관계의 코드를 하나의 HTML에 담는 형태로 코드 작성.
```

---

## ✨ 주요 특징

- 🚙 **차체 + 2륜 구조** — 직사각형 chassis + 두 원형 바퀴, Matter.js 공식 Car 패턴
- 🪨 **절차적 지형** — `Bodies.fromVertices` + `poly-decomp`로 concave 폴리라인 충돌 정확히 처리
- 〰️ **스프링/댐퍼** — `stiffness` + `damping` 튜닝으로 출렁임과 흡수율 표현
- ⚡ **드라이빙 물리** — 가속·브레이크·후진 + 관성 모멘텀 자연 반영
- 🎮 **조작감** — 화살표/WASD/스페이스바/R/C, 카메라가 차체 추적
- 📦 **단일 HTML** — CDN 2개만, 외부 빌드 도구 없음
- 🔒 **온디바이스** — 모든 물리가 브라우저 안에서 처리됨 (서버 0)

---

## 🚀 실행 방법

### 방법 1: 라이브 데모 (GitHub Pages, 가장 간단)
위 "라이브 데모" 섹션의 URL을 브라우저에서 열기. CDN 2개가 자동 로드됩니다.

### 방법 2: 브라우저로 직접 열기
```bash
open index.html        # macOS
xdg-open index.html    # Linux
start index.html       # Windows
```

### 방법 3: 로컬 정적 서버 (권장 — CDN 로깅 깨끗)
```bash
python3 -m http.server 8000
# → http://localhost:8000 접속
```

> **참고**: matter-js + poly-decomp는 jsDelivr CDN에서 로드됩니다. 오프라인 환경에서는 `index.html`의 `<script src=...>` 라인을 로컬 경로로 교체하세요.

---

## 🎮 조작법

| 입력 | 동작 |
|---|---|
| **→ / D** | 가속 / 전진 (바퀴에 토크 인가) |
| **← / A** | 브레이크 / 후진 |
| **스페이스바** | 핸드브레이크 (마찰력 ↑) |
| **R 키** | 차량 + 지형 리셋 |
| **C 키** | 카메라 추적 모드 토글 |

---

## 🛠️ 기술 스택

| 영역 | 사용 기술 |
|---|---|
| **물리 엔진** | Matter.js 0.20.0 (CDN) — `Bodies.fromVertices`, `Constraint`, `Engine.update` |
| **폴리곤 분해** | poly-decomp 0.3.0 (CDN) — concave terrain용 |
| **렌더링** | Canvas 2D (Matter.Render 커스텀 루프) |
| **카메라** | `viewTransform` + 차체 추적 (C 키 토글) |
| **입력** | 키보드 리스너 + 회전 토크 적용 |
| **번들링** | 없음 (단일 HTML + CDN 2개) |
| **언어** | Vanilla JavaScript (ES6+) |

---

## 📂 프로젝트 구조

```
offroad-suspension/
├── index.html      # 단일 HTML (모든 코드 + CDN script 태그 2개)
├── README.md       # 한국어 (기본)
├── README.en.md    # English (옵션)
└── LICENSE         # MIT
```

---

## 🎨 디자인 결정

브레인스토밍 단계에서 내린 결정 6가지:

| 결정 포인트 | 선택 | 이유 |
|---|---|---|
| **물리 엔진** | Matter.js (CDN) | 2D 강체 + Constraint API가 차량 서스펜션에 가장 직관적 |
| **차체 형태** | 직사각형 + 두 원형 바퀴 | 공식 Car 예제 패턴, density 차이로 무게중심 자연스러움 |
| **스프링/댐퍼** | Constraint 튜닝 (`stiffness` 0.05~0.15, `damping` 0.1~0.3) | 진동 ↔ 처짐 트레이드오프 최적점 |
| **지형** | 절차적 폴리라인 + `poly-decomp` | concave 분해 정확성, 정적 바디로 충돌 비용 ↓ |
| **카메라** | `viewTransform` + 차체 추적 (C 토글) | 큰 지형에서도 차량이 화면 중앙 유지 |
| **번들링** | 없음 (단일 HTML + CDN 2개) | 오프라인/내부 호스팅 즉시 전환 가능 |

### 직접 커스터마이즈하고 싶다면

`index.html` 상단에서 다음 상수를 조정하면 물리/조작감을 바꿀 수 있어요:

```js
const CONFIG = {
  // 차체/바퀴
  CHASSIS_W: 90,           // 차체 가로 길이
  CHASSIS_H: 30,           // 차체 세로 길이
  WHEEL_R: 18,             // 바퀴 반지름
  
  // 스프링/댐퍼 (핵심)
  SUSPENSION_STIFFNESS: 0.1,   // 0.05~0.15 (낮을수록 부드러움)
  SUSPENSION_DAMPING: 0.2,     // 0.1~0.3 (높을수록 흡수 잘됨)
  SUSPENSION_LENGTH: 20,       // 스프링 자연 길이 (살짝 남겨 압축 가능)
  
  // 지형
  TERRAIN_SEED: 42,        // 절차적 노이즈 시드
  TERRAIN_AMPLITUDE: 80,   // 절벽 높이
  TERRAIN_SEGMENTS: 200,   // 폴리라인 해상도
  
  // 드라이빙
  DRIVE_TORQUE: 0.04,      // 가속 토크
  BRAKE_TORQUE: -0.03,     // 브레이크 토크
  HANDBRAKE_FRICTION: 0.95, // 핸드브레이크 마찰 계수
};
```

`SUSPENSION_STIFFNESS`를 0.05로 낮추면 부드러운 승차감, 0.15로 올리면 단단한 레이싱카 느낌. `SUSPENSION_DAMPING`은 출렁임이 가라앉는 속도를 결정합니다.

---

## 🧠 동작 원리

```
차체(Chassis, 직사각형)
   │
   ├── Constraint(스프링/댐퍼) ── 왼쪽 바퀴 (circle)
   │       stiffness 0.1, damping 0.2, length 20
   │       ↳ 차체-바퀴 거리/각도 보정 → 진동 흡수
   │
   └── Constraint(스프링/댐퍼) ── 오른쪽 바퀴 (circle)
           stiffness 0.1, damping 0.2, length 20

매 프레임 Matter.Engine.update():
  1. 중력 적용 → 바퀴가 terrain에 닿음
  2. Constraint가 차체-바퀴 거리/각도 보정 → 스프링 압축/신장
  3. damping이 진동 감쇠 → 댐퍼 흡수
  4. 키보드 입력 시 바퀴에 토크 인가 → 전진/후진
  5. camera.transform이 차체 위치 추적
```

**왜 `poly-decomp`가 필요한가**: Matter.js의 `Bodies.fromVertices`는 convex 폴리곤만 직접 처리 가능. 절벽 같은 concave 폴리라인은 먼저 `poly-decomp`로 convex 분해한 다음에 Matter.js에 넘겨야 정확한 충돌이 계산됩니다. CDN 로드 순서가 중요 — `poly-decomp`가 `matter-js`보다 **먼저** 로드되어야 합니다.

---

## 🔬 검증

| 항목 | 값 |
|---|---|
| **로컬 index.html** | 40,632 B |
| **GitHub Pages 응답** | HTTP 200 · 40,632 B (bit-perfect match) |
| **의존성** | matter-js 0.20.0, poly-decomp 0.3.0 (jsDelivr CDN) |
| **렌더링** | Canvas 2D, 60fps (Matter.Render) |
| **물리 step** | `Engine.update()` 60Hz |
| **앵커 깨짐** | 0개 (KR/EN 혼합 헤딩 0) |

---

## 📝 프롬프트 이력

| 차수 | 시점 | 작업 |
|---|---|---|
| 1차 | 2026-07-08 17:00 | 코딩미션 scaffolding — README + placeholder index.html |
| 2차 | 2026-07-08 17:55 | OpenCode가 Matter.js 시뮬레이터 본체 구현 (s1~s4 4단계 디버깅) |
| 3차 | 2026-07-09 06:50 | fix1~fix22 — 스프링/댐퍼 안정화 + trackbar 추가, 완전 정착 |
| 4차 | 2026-07-09 08:55 | 초기 배포 + README 다층 v1.0 (현재) |

---

## 📜 License

MIT © 2026 sigco3111

---

## 🙏 Acknowledgments

이 프로젝트는 [MiniMax-M3](https://example.com) 모델과 OpenCode CLI 환경에서 생성되었습니다. 프롬프트 엔지니어링과 디자인 결정은 저장소 소유자가 직접 수행했습니다.

- **코딩미션 참조 페이지**: [cokac.com — 코드깎는노인](https://cokac.com/list/announcement/24)
