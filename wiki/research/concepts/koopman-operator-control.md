---
title: "Koopman Operator 기반 MPC"
type: concept
tags: [Koopman operator, MPC, EDMD, lifting, linear representation, nonlinear systems, data-driven control]
papers: [zhang-2026-koopman-mpc-time-delayed]
last_updated: 2026-06-24
---

## 한 줄 요약

**비선형 시스템을 고차원 선형 시스템으로 변환**하여, NMPC의 비선형 최적화(NLP) 대신 **선형 MPC의 빠른 QP 최적화**를 그대로 쓰는 방법론.

---

## 핵심 아이디어: 왜 Koopman인가?

MPC를 이미 잘 알고 있다면, 다음 딜레마가 친숙할 것이다:

> - **선형 MPC**: QP로 빠름. 그러나 선형화 오차 — 넓은 동작 범위에서 모델 부정확.
> - **NMPC**: 비선형 모델 그대로 사용하니 정확. 그러나 NLP 풀어야 해서 느림 — 임베디드 실시간 구현 어려움.

Koopman MPC의 제안: **비선형 상태공간을 "들어올려서(lifting)"** 선형이 되는 공간을 찾자.

---

## Koopman 연산자란?

수학적으로, Koopman 연산자 K는 **상태 x 위의 함수(observable)에 작용하는 무한차원 선형 연산자**다. 직관적으로:

```
비선형 시스템:    x_{k+1} = f(x_k, u_k)       ← 비선형, 저차원
Koopman 관점:  φ(x_{k+1}) = K · φ(x_k) + B · u_k  ← 선형,  고차원
```

여기서 **φ(x)** 는 관측 함수(observable) 벡터 — 상태 x의 비선형 변환들의 모음.

### 핵심 통찰
- **x** 를 직접 다루지 않고, **φ(x) = [φ₁(x), φ₂(x), ..., φₙ(x)]** 라는 새로운 "좌표계"로 봄
- 이 좌표계에서 동역학이 **선형**이 됨
- 일종의 비선형 좌표 변환 — Feedback Linearization과 개념적으로 유사하지만, **데이터로부터 자동 학습**

---

## 기존 MPC와 비교

| 항목 | 기존 선형 MPC | NMPC | **Koopman MPC** |
|------|-------------|------|----------------|
| 플랜트 모델 | 선형화 모델 (동작점 근방 유효) | 비선형 FP 모델 | 데이터로 학습한 선형 Koopman 모델 |
| 최적화 | **QP** (빠름, ∼ms) | **NLP** (느림, ∼수십ms) | **QP** (빠름) |
| 비선형 처리 | 선형화 오차 존재 | 정확 | Lifting 공간에서 선형 근사 |
| 모델 출처 | 물리 + 선형화 | 물리 방정식 | **실험 데이터** (EDMD) |
| 파라미터 동정 | 물리 기반 | 물리 기반 | **데이터 기반** |
| 동작 범위 | 선형화점 근방 제한 | 전 범위 | 학습 데이터 커버 범위 |
| 실시간 구현 | 쉬움 | 어려움 | **쉬움** (QP이므로) |
| 불확실성 처리 | 강인 MPC로 확장 가능 | NMPC에 통합 | Zhang(2026): **온라인 불확실 집합 갱신** |

> **결론**: Koopman MPC는 "비선형 NMPC의 정확도 + 선형 MPC의 속도"를 동시에 얻으려는 시도.

---

## 어떻게 구현하는가? (3단계)

### Step 1. Observable 함수 φ(x) 선택
상태 x = [v, ω, T, ...] 에 대해 관측 함수 기저를 선택:
- 다항식: φ(x) = [x₁, x₂, x₁², x₁x₂, x₂², ...]
- RBF (가우시안 함수)
- Fourier 기저
- 신경망 (Deep Koopman)

선택이 Koopman MPC 성능의 핵심 — 잘못 선택하면 선형 근사 오차 큼.

### Step 2. EDMD (Extended Dynamic Mode Decomposition)로 모델 학습
데이터 수집: {(xₖ, uₖ, xₖ₊₁)} N개 스냅샷

최소제곱으로 A, B 행렬 추정:
```
min ||Φ' - A·Φ - B·U||²_F
```
- Φ = [φ(x₀), φ(x₁), ..., φ(x_{N-1})]  ← lifting된 상태 스냅샷 행렬
- Φ' = [φ(x₁), φ(x₂), ..., φ(x_N)]     ← 한 스텝 후 상태
- U = [u₀, u₁, ..., u_{N-1}]

결과: **φ(xₖ₊₁) ≈ A·φ(xₖ) + B·uₖ** (선형 시스템!)

### Step 3. 선형 MPC 적용
이제 우리가 익숙한 선형 MPC 그대로:
```
min  Σ [ ||φ(x) - φ(x_ref)||²_Q + ||u||²_R ]
s.t. φ(xₖ₊₁) = A·φ(xₖ) + B·uₖ
     u_min ≤ u ≤ u_max
     φ(x) ∈ ℱ  (상태 제약)
```
**QP 풀면 끝.** 선형 MPC와 동일한 형식.

---

## Zhang (2026)이 추가한 것: 시간지연 + 온라인 불확실 집합

[[zhang-2026-koopman-mpc-time-delayed]]는 기존 Koopman MPC에 두 가지를 더했다:

### ① 시간지연 처리
CAN 버스, 센서 지연 등으로 실제 시스템은 `u(t-τ)` 형태의 지연 입력이 있음. 해결책: 지연 상태도 observable에 포함시켜 lifting:
```
φ_delay(xₖ) = [φ(xₖ), φ(xₖ₋₁), ..., φ(xₖ₋ₘ), uₖ₋₁, ..., uₖ₋ₘ]
```
→ 지연 포함 선형 시스템으로 변환.

### ② 고정 불확실 집합의 보수성 제거
기존 강인 Koopman MPC: 불확실 집합 W을 사전에 최악의 경우로 고정 → 너무 보수적, 실제 성능 저하.

Zhang (2026): 불확실 집합을 **현재 상태와 입력에 따라 온라인으로 갱신** → 덜 보수적, 강인성 유지.

---

## Koopman MPC vs. PINN 기반 MPC (비교)

[[habich-2026-pinn-mpc-soft-robot]]과 비교하면 두 방법론의 철학이 다름:

| 항목 | Koopman MPC | PINN 기반 MPC (DD-PINN) |
|------|------------|------------------------|
| 모델 출처 | 실험 데이터 (EDMD) | 물리 방정식 (FP 모델 + collocation) |
| 물리 법칙 | 반영 안 됨 (순수 데이터) | **내재화** (physics loss) |
| 최적화 형식 | **QP** (볼록, 빠름) | NLP (비볼록, 느림) |
| 그래디언트 | 해석적 (선형 행렬) | 해석적 (DD-PINN 앤사츠) 또는 자동미분 |
| 데이터 필요량 | 많음 (EDMD 데이터셋) | 적음 또는 없음 (FP 시뮬레이션) |
| 도메인 변화 | 재학습 필요 | δ 변수로 일반화 가능 |
| 강인성 보장 | 이론적 (Zhang 2026) | 없음 (경험적) |

---

## 언제 사용하는가?

### Koopman MPC가 적합한 상황
- ✅ **실험 데이터가 충분**하고 FP 모델 구축이 어려운 시스템
- ✅ **빠른 계산이 필요** (임베디드 제어기, 100 Hz+)
- ✅ **CAN 버스 시간지연**이 있는 차량 제어 (Zhang 2026이 직접 다룸)
- ✅ 넓은 동작 범위에서 선형화가 부정확한 비선형 시스템
- ✅ 강인성 보장이 필요한 경우 (강인 Koopman MPC로 확장)

### 주의가 필요한 상황
- ⚠️ Observable 기저 선택에 도메인 지식 필요 — 잘못 선택 시 근사 오차 큼
- ⚠️ 상태 차원이 매우 높으면 lifting 후 차원 폭발
- ⚠️ 학습 데이터 범위를 벗어난 외삽 불안정
- ⚠️ 물리 법칙 위반 가능성 (데이터 기반이므로)

---

## 교수님 연구와의 연결점

| 연구 영역 | Koopman MPC 적용 가능성 |
|---------|----------------------|
| EV 파워트레인 최적 제어 | HEV 배터리-모터 비선형 동역학 → Koopman lifting + QP |
| 회생제동 토크 제어 | CAN 버스 지연 있는 제동 명령 → Zhang(2026) 직접 적용 |
| 차량 상태 추정 | Koopman 관측기 (KO-EKF) — lifting 공간에서 칼만 필터 |
| 통합 섀시 제어 | Koopman + 파티셔닝 → [[adaptive-partitioning-ev-chassis]] |

특히 **회생제동 제어**에서 CAN 버스 시간지연은 교수님 연구에서 실제로 마주치는 문제이고, Zhang(2026)이 이를 직접 해결하는 프레임워크를 제공하므로 연결성이 높음.

---

## 관련 페이지

- [[zhang-2026-koopman-mpc-time-delayed]] — 시간지연 + 온라인 불확실 집합 Koopman MPC
- [[physics-informed-neural-networks]] — 대안 방법론 (PINN 기반 서로게이트 MPC)
- [[noncentralized-mpc]] — Koopman과 분산 MPC 결합
- [[adaptive-partitioning-ev-chassis]] — Koopman + 적응형 파티셔닝 연구 아이디어
- [[pinn-surrogate-ev-nmpc]] — Koopman과 비교되는 PINN 서로게이트 접근법
