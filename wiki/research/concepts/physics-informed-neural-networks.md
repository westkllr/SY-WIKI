---
title: "Physics-Informed Neural Networks (PINNs)"
type: concept
tags: [PINN, surrogate model, neural networks, differential equations, physics-based learning, NMPC]
papers: [habich-2026-pinn-mpc-soft-robot, labib-2026-battery-voltage-dmdc-transformer]
last_updated: 2026-06-24
---

## 개요

Physics-Informed Neural Networks(PINNs)는 신경망 학습 시 지배 미분방정식(ODE/PDE)을 손실 함수의 물리 항(physics residual loss)으로 포함시켜, 적은 데이터로도 물리 법칙을 준수하는 근사 해를 학습하는 방법론. Raissi et al. (2019, JCP)이 기초를 확립했으며, 이후 제어·로봇·에너지 시스템으로 빠르게 확산.

## 핵심 변형

### 원본 PINN (Raissi et al.)
- 입력: 공간·시간 좌표 (x, t)
- 손실: 데이터 손실 + 물리 잔차 손실 + 경계 조건 손실
- 제어 적용 한계: 초기 조건 변경 시 재학습 필요

### PINC (Physics-Informed Neural Control)
- 초기 조건 x₀와 입력 u도 네트워크 입력으로 받음
- 상태 전이 함수 Φ: (x₀, u, t) → x(t) 학습
- NMPC에서 implicit differentiation으로 그래디언트 계산
- 참고: [[habich-2026-pinn-mpc-soft-robot]]

### DD-PINN (Domain-Decoupled PINN)
- 앤사츠 구조: x̂(t) = x₀ + t · φ(x₀, u, t; θ)
  - 초기 조건 x̂(0) = x₀ 자동 만족
  - 시간 미분 ∂x̂/∂t = φ + t · ∂φ/∂t (해석적 계산 가능)
- NMPC 그래디언트를 closed-form으로 계산 → PINC 대비 빠름
- 도메인 변수 δ를 추가 입력으로 받아 도메인 일반화 지원
- 참고: [[habich-2026-pinn-mpc-soft-robot]]

## 학습 데이터 특성

| 항목 | 내용 |
|------|------|
| Collocation points | 미분방정식이 만족되어야 할 시공간 샘플점 |
| 실제 측정 데이터 | 소량 또는 없음 — FP 시뮬레이션으로 대체 가능 |
| 물리 잔차 | ODE: dẋ/dt − f(x, u) = 0 이 되도록 penalize |
| 경계/초기 조건 | 별도 손실 항으로 강제 또는 앤사츠로 자동 만족 |

## 제어 시스템 응용 시 장점

- 데이터 효율성 — 실험 데이터 없이 FP 모델만으로 학습 가능
- 추론 속도 — 학습 후 forward pass: μs 수준 (FP 모델 ms 대비 100–1000× 빠름)
- 도메인 일반화 — δ 변수를 통해 시스템 파라미터 변화 처리
- 미분 가능성 — NMPC 그래디언트 계산에 직접 활용

## 제어 시스템 응용 시 한계

- 학습 시간 길다 (수일, GPU 필요)
- FP 모델 필요 (완전 데이터 기반 아님)
- 온라인 적응 어려움 (실시간 재학습 비현실적)
- 고차원 시스템에서 collocation point 수 폭발

## 차량 동역학 적용 사례

- Zeipel, Habich, Seel, Ehlers (2024, TechRxiv): "Fast and accurate prediction of vehicle dynamics using physics-informed neural networks" — [[habich-2026-pinn-mpc-soft-robot]] 참고문헌 [71]. 동일 Leibniz Hannover 그룹. **우선 ingest 대상.**

## 관련 개념

- [[noncentralized-mpc]] — PINN 서로게이트와 결합해 분산 MPC 속도 향상 가능
- [[graph-partitioning-control]] — 분산 시스템에서 PINN 서브시스템 모델링

## 관련 연구 아이디어

- [[pinn-surrogate-ev-nmpc]] — EV 파워트레인 NMPC에 DD-PINN 서로게이트 적용
