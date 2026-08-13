# 🏔️ offroad-suspension

> 2D off-road car suspension simulator built on HTML5 Canvas + Matter.js

A 2D off-road car driving over jagged cliff terrain. **Spring/damper (Shock Absorber) Constraints between chassis and wheels** absorb terrain shocks, and acceleration / braking reflect natural inertia momentum. Reset with R, drive with arrow keys / WASD, and the camera smoothly tracks the vehicle.

[🇰🇷 한국어](./README.md) · [🇺🇸 English (default)](#)

---

## 🎬 Live Demo

> **👉 [https://sigco3111.github.io/offroad-suspension/](https://sigco3111.github.io/offroad-suspension/)** — Run directly in the browser (60fps, Matter.js CDN)

| | |
|---|---|
| ![Demo](https://img.shields.io/badge/Live-Demo-222222?style=for-the-badge&logo=githubpages&logoColor=white) | [![Repo](https://img.shields.io/badge/GitHub-sigco3111%2Foffroad--suspension-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/sigco3111/offroad-suspension) |
| ![Status](https://img.shields.io/badge/Status-Live-22C55E?style=flat-square) | ![Stack](https://img.shields.io/badge/Stack-Matter.js-F7DF1E?style=flat-square&logo=javascript&logoColor=black) |
| ![License](https://img.shields.io/badge/License-MIT-F1C40F?style=flat-square) | ![Deps](https://img.shields.io/badge/Dependencies-2_CDN-9CA3AF?style=flat-square) |

### 🎮 Quick usage
1. Click the demo link above → page opens in your browser
2. **→ / D** — Accelerate (forward)
3. **← / A** — Brake / reverse
4. **Space** — Handbrake (friction ↑)
5. **R** — Reset vehicle + terrain
6. **C** — Toggle camera follow mode

---

## 🤖 Attribution

This project's code was **auto-generated** using the model and prompt below.

| Item | Value |
|---|---|
| **Model** | MiniMax-M3 |
| **Runtime** | OpenCode CLI |
| **Repository** | [`sigco3111/offroad-suspension`](https://github.com/sigco3111/offroad-suspension) |
| **License** | MIT |
| **Dependencies** | 2 (matter-js@0.20.0, poly-decomp@0.3.0 — both via jsDelivr CDN) |

### 📝 Prompt used (verbatim, KR)

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

## ✨ Features

- 🚙 **Chassis + 2 wheels** — Rectangular chassis + two circular wheels (Matter.js canonical car pattern)
- 🪨 **Procedural terrain** — `Bodies.fromVertices` + `poly-decomp` for accurate concave polyline collisions
- 〰️ **Spring/damper** — `stiffness` + `damping` tuning for oscillation and absorption
- ⚡ **Driving physics** — Accel / brake / reverse + natural inertia momentum
- 🎮 **Controls** — Arrow / WASD / Space / R / C, camera tracks vehicle
- 📦 **Single HTML** — 2 CDN deps only, no build step
- 🔒 **On-device** — All physics runs in the browser (zero server)

---

## 🚀 Quick Start

### Option 1: Live demo (GitHub Pages, easiest)
Open the URL in the "Live Demo" section above. Both CDN scripts load automatically.

### Option 2: Open directly in a browser
```bash
open index.html        # macOS
xdg-open index.html    # Linux
start index.html       # Windows
```

### Option 3: Local static server (recommended — cleaner CDN logs)
```bash
python3 -m http.server 8000
# → http://localhost:8000
```

> **Note**: matter-js + poly-decomp are loaded from jsDelivr CDN. For offline use, replace the `<script src=...>` lines in `index.html` with local paths.

---

## 🎮 Controls

| Input | Action |
|---|---|
| **→ / D** | Accelerate / forward (apply torque to wheels) |
| **← / A** | Brake / reverse |
| **Space** | Handbrake (friction ↑) |
| **R** | Reset vehicle + terrain |
| **C** | Toggle camera follow mode |

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| **Physics engine** | Matter.js 0.20.0 (CDN) — `Bodies.fromVertices`, `Constraint`, `Engine.update` |
| **Polygon decomposition** | poly-decomp 0.3.0 (CDN) — for concave terrain |
| **Rendering** | Canvas 2D (Matter.Render custom loop) |
| **Camera** | `viewTransform` + chassis tracking (C key toggle) |
| **Input** | Keyboard listener + rotational torque |
| **Bundling** | None (single HTML + 2 CDN scripts) |
| **Language** | Vanilla JavaScript (ES6+) |

---

## 📂 Project Structure

```
offroad-suspension/
├── index.html      # Single HTML (all code + 2 CDN script tags)
├── README.md       # Korean (default)
├── README.en.md    # English (this file)
└── LICENSE         # MIT
```

---

## 🎨 Design Choices

Six decisions from the brainstorming stage:

| Decision | Choice | Rationale |
|---|---|---|
| **Physics engine** | Matter.js (CDN) | 2D rigid body + Constraint API is the most intuitive fit for car suspension |
| **Chassis shape** | Rectangle + two circular wheels | Canonical Car pattern, density contrast gives natural center-of-mass behaviour |
| **Spring/damper** | Constraint tuning (`stiffness` 0.05~0.15, `damping` 0.1~0.3) | Sweet spot between oscillation and sag |
| **Terrain** | Procedural polyline + `poly-decomp` | Accurate concave decomposition, static body for low collision cost |
| **Camera** | `viewTransform` + chassis tracking (C toggle) | Vehicle stays centered on screen even on large terrain |
| **Bundling** | None (single HTML + 2 CDN deps) | Instant offline / internal hosting swap |

### Want to customize?

Tweak these constants near the top of `index.html` to change physics & feel:

```js
const CONFIG = {
  // Chassis / wheels
  CHASSIS_W: 90,           // chassis width
  CHASSIS_H: 30,           // chassis height
  WHEEL_R: 18,             // wheel radius

  // Spring / damper (core)
  SUSPENSION_STIFFNESS: 0.1,   // 0.05~0.15 (lower = softer)
  SUSPENSION_DAMPING: 0.2,     // 0.1~0.3 (higher = absorbs more)
  SUSPENSION_LENGTH: 20,       // natural spring length (slight gap so it can compress)

  // Terrain
  TERRAIN_SEED: 42,        // procedural noise seed
  TERRAIN_AMPLITUDE: 80,   // cliff height
  TERRAIN_SEGMENTS: 200,   // polyline resolution

  // Driving
  DRIVE_TORQUE: 0.04,      // accel torque
  BRAKE_TORQUE: -0.03,     // brake torque
  HANDBRAKE_FRICTION: 0.95, // handbrake friction coefficient
};
```

`SUSPENSION_STIFFNESS` 0.05 → soft ride; 0.15 → stiff race-car feel. `SUSPENSION_DAMPING` controls how fast the oscillation dies down.

---

## 🧠 How It Works

```
Chassis (rectangle)
   │
   ├── Constraint (spring/damper) ── Left wheel (circle)
   │       stiffness 0.1, damping 0.2, length 20
   │       ↳ corrects chassis-wheel distance/angle → absorbs shock
   │
   └── Constraint (spring/damper) ── Right wheel (circle)
           stiffness 0.1, damping 0.2, length 20

Each frame, Matter.Engine.update():
  1. Apply gravity → wheels touch terrain
  2. Constraints correct chassis-wheel distance/angle → spring compresses/extends
  3. damping attenuates oscillation → damper absorbs
  4. Keyboard input applies torque to wheels → forward/reverse
  5. camera.transform tracks chassis position
```

**Why `poly-decomp`?** Matter.js's `Bodies.fromVertices` only handles convex polygons directly. Cliff-like concave polylines must first be decomposed into convex pieces by `poly-decomp` before being handed to Matter.js. CDN load order matters — `poly-decomp` **must load before** `matter-js`.

---

## 🔬 Verification

| Item | Value |
|---|---|
| **Local index.html** | 40,632 B |
| **GitHub Pages response** | HTTP 200 · 40,632 B (bit-perfect match) |
| **Dependencies** | matter-js 0.20.0, poly-decomp 0.3.0 (jsDelivr CDN) |
| **Rendering** | Canvas 2D, 60fps (Matter.Render) |
| **Physics step** | `Engine.update()` 60Hz |
| **Anchor breaks** | 0 (no KR/EN mixed headings) |

---

## 📝 Prompt Log

| # | When | Task |
|---|---|---|
| 1 | 2026-07-08 17:00 | Coding-mission scaffold — README + placeholder index.html |
| 2 | 2026-07-08 17:55 | OpenCode built the Matter.js simulator body (s1~s4 four-stage debug) |
| 3 | 2026-07-09 06:50 | fix1~fix22 — spring/damper stabilisation + trackbar added, fully settled |
| 4 | 2026-07-09 08:55 | Initial deploy + multi-layer README v1.0 (current) |

---

## 📜 License

MIT © 2026 sigco3111

---

## 🙏 Acknowledgments

This project was generated with the [MiniMax-M3](https://example.com) model in the OpenCode CLI environment. Prompt engineering and design choices were performed directly by the repository owner.

- **Coding-mission reference page**: [cokac.com — 코드깎는노인](https://cokac.com/list/announcement/24)
