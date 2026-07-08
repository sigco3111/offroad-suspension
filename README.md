# 🏔️ 2D Off-Road Suspension Simulator

> 울퉁불퉁한 지형을 달리는 2D 오프로드 자동차. 바퀴-차체 사이 스프링/댐퍼(Shock Absorber) 서스펜션 물리학으로 지형 충격을 흡수하고, 가속·제동 시 관성 모멘텀이 계산된 드라이빙 시뮬레이터.

---

## 🎬 라이브 데모 (Live Demo)

- **GitHub Pages**: https://sigco3111.github.io/offroad-suspension/ (배포 후 활성화)
- 로컬 실행: `index.html` 더블클릭 또는 `python3 -m http.server 8000`

---

## 🤖 생성 정보 (Attribution)

이 프로젝트의 코드는 **OpenCode CLI** + **MiniMax-M3** 모델로 생성되었습니다.

- **Tool**: [OpenCode](https://github.com/snymann/opencode) (AI 코딩 어시스턴트)
- **Model**: MiniMax-M3 (provider: minimax)
- **Generation mode**: 단일 HTML 임베드 (CDN 의존성 포함, 모든 의존관계 코드 1파일)

프롬프트 원문은 본 README 하단 "프롬프트 이력" 절 참조.

---

## ✨ 주요 특징 (Features)

- 🚙 **오프로드 자동차** — 차체(Chassis) + 두 바퀴(Wheels) + 스프링/댐퍼 Constraints
- 🪨 **울퉁불퉁한 지형** — 절차적 또는 정적 폴리라인 terrain, 충돌 정확히 처리
- 〰️ **서스펜션 흡수** — `stiffness`(스프링) + `damping`(댐퍼) 튜닝으로 출렁임 표현
- ⚡ **드라이빙 물리** — 가속 페달·브레이크·후진 + 관성 모멘텀 자연 반영
- 🎮 **조작감** — 화살표/WASD로 직관적 운전, 카메라가 차체 추적
- 🌐 **단일 HTML** — 외부 빌드 도구 없이 브라우저에서 바로 실행

---

## 🚀 실행 방법 (Quick Start)

```bash
# 옵션 A: 브라우저에서 직접 열기
open index.html

# 옵션 B: 로컬 정적 서버 (권장 — CDN 로깅 깨끗)
python3 -m http.server 8000
# → http://localhost:8000 접속
```

> **참고**: Matter.js는 CDN(`https://cdn.jsdelivr.net`)에서 로드됩니다. 오프라인 환경에서는 `index.html`의 `<script src=...>` 라인을 로컬 경로로 교체하세요.

---

## 🎮 조작법 (Controls)

| 입력 | 동작 |
|---|---|
| **← / A** | 브레이크 / 후진 |
| **→ / D** | 가속 / 전진 |
| **스페이스바** | 핸드브레이크 (마찰력 ↑) |
| **R 키** | 차량 + 지형 리셋 |
| **C 키** | 카메라 추적 모드 토글 |

---

## 🛠️ 기술 스택 (Tech Stack)

| 분류 | 선택 |
|---|---|
| **물리 엔진** | Matter.js (CDN, `Bodies.fromVertices` + `Constraint`) |
| **렌더링** | Canvas 2D (Matter.Render) |
| **카메라** | Matter.Bounds + 변환 행렬 (차체 추적) |
| **입력** | 키보드 리스너 + 회전 토크 적용 |
| **번들링** | 없음 (단일 HTML) |
| **언어** | Vanilla JavaScript (ES6+) |

---

## 🎨 디자인 결정 (Design Choices)

1. **단일 HTML 임베드** — `canvas-static-site-pipeline` 패턴 준수. CDN URL만 바꾸면 오프라인/내부 호스팅 즉시 전환 가능.
2. **차체 = 직사각형 + 두 원형 바퀴** — Matter.js 공식 Car 예제 패턴. `density`로 무게중심 차체 쪽에 두어 출렁임 자연스러움.
3. **스프링/댐퍼 = Constraint 튜닝** — `stiffness: 0.05~0.15` (너무 높으면 진동, 너무 낮으면 처짐), `damping: 0.1~0.3` (흡수율). 일반 Constraint와 다른 핵심은 `length` 살짝 남겨 압축 가능하게.
4. **회전 = 토크 적용** — 바퀴에 `Body.setAngularVelocity`나 직접 토크 인가. `friction: 0.9`로 접지력 확보.
5. **관성 모멘텀** — 차체 density > 바퀴 density로 자연스러운 전후 기울임. 브레이크 시 무게중심 이동 표현.
6. **카메라 변환** — Render 옵션의 `bounds` 또는 `viewTransform`으로 차체 추적. 큰 지형에서도 차가 화면 중앙 유지.

---

## 🧠 동작 원리 (How It Works)

```
차체(Chassis) ──┬── Constraint ── 왼쪽 바퀴 (circle)
                │      ↳ stiffness 0.1, damping 0.2, length 20 (스프링/댐퍼)
                │
                └── Constraint ── 오른쪽 바퀴 (circle)
                       ↳ stiffness 0.1, damping 0.2, length 20

매 프레임 Matter.Engine.update():
  1. 중력 적용 → 바퀴가 terrain에 닿음
  2. Constraint가 차체-바퀴 거리/각도 보정 → 스프링 압축/신장
  3. damping이 진동 감쇠 → 댐퍼 흡수
  4. 사용자 입력 → 바퀴에 토크/각속도 → 추진
  5. 차체는 바퀴에서 전달받은 힘으로 출렁이며 따라감 (관성 모멘텀)
  6. 카메라가 차체 위치 추적
```

핵심은 **Constraint의 `stiffness` × `damping` 조합**입니다.
- `stiffness` ↑: 딱딱한 레이싱카 (지형 그대로 전달)
- `stiffness` ↓ + `damping` ↑: 부드러운 오프로드 SUV (충격 흡수)
- `damping` ↓: 쿠션 같고 출렁임 오래 감 (오버스쿼시)

---

## 🔬 검증 (Verification)

- `python3 -m http.server`로 로컬 서빙 후 페이지 로드 확인
- 화살표로 가속 → 차가 전진하며 바퀴 회전
- 지형 절벽에서 → 차체 출렁이며 충격 흡수
- 브레이크 → 무게중심 앞으로 쏠림 (관성 표현)
- 콘솔 에러 0개 확인
- 비트-퍼펙트 사이즈: `curl -sS -w "%{size_download}" -o /dev/null http://localhost:8000/` ≡ `wc -c < index.html`

---

## 📝 프롬프트 이력 (Prompt Log)

원본 미션 지시 (2026-07-08):

> 울퉁불퉁한 지형 위를 달리는 2D 오프로드 자동차를 구현하되, 바퀴와 차체 사이에 스프링과 댐퍼(Shock Absorber)가 달린 서스펜션 물리학을 적용하여 지형의 충격을 흡수하며 차체가 출렁거리는 모습을 보여주고, 가속과 제동 시의 관성 모멘텀까지 계산된 드라이빙 시뮬레이터를 코딩해줘.
>
> **Implementation Advice**: Use **Matter.js**. The "Car" module is a classic example. Connect two wheels (circles) to a chassis (rectangle) using standard Constraints with `stiffness` and `damping` properties to simulate shock absorbers. 모든 의존관계의 코드를 하나의 HTML에 담는 형태로 코드 작성.

---

## 📄 License

MIT