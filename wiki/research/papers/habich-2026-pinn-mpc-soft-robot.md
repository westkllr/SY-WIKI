---
title: "Generalizable and Fast Surrogates: Model Predictive Control of Articulated Soft Robots Using Physics-Informed Neural Networks"
type: paper
authors: [Habich, Tim-Lukas, Mohammad, Aran, Ehlers, Simon F. G., Bensch, Martin, Seel, Thomas, Schappler, Moritz]
year: 2026
journal: IEEE Transactions on Robotics
doi: 10.1109/TRO.2025.3631818
tags: [physics-informed neural networks, PINN, NMPC, surrogate model, domain generalization, soft robot, model predictive control]
methods: [PINC, DD-PINN, GRU-RNN, Euler-Lagrange, ASHA HPO, CasADi, PyTorch]
source_file: raw/papers/2026TRO_Habich.pdf
has_full_text: true
last_updated: 2026-06-24
---

## Abstract

소프트 로봇의 복잡한 비선형 동역학을 실시간 NMPC에 활용하기 위해 PINN 기반 서로게이트 모델(PINC, DD-PINN)을 5-DoF 관절형 공압 소프트 로봇에 최초 적용한 논문. 훈련 이후 미지의 시스템 도메인(다른 부하·방향)으로 일반화하는 도메인 변수 δ를 도입해, 단 1개 도메인 학습으로 12개 미지 도메인에서 PI 대비 14.6% 오차 감소를 달성하며 47 Hz NMPC를 실현.

## Key Contributions

- **최초 실증**: 원본 PINN, PINC, DD-PINN을 실제 다자유도(5-DoF) 소프트 로봇에 최초 적용 및 비교
- **도메인 일반화**: 도메인 변수 δ를 PINC·DD-PINN에 확장 — 훈련 후 시스템 파라미터 변화(하중, 방향)에 일반화 가능
- **DD-PINN 앤사츠 함수**: 해법 x̂(t) = x₀ + t · φ(x₀, u, t, δ; θ) 구조로 초기 조건 자동 만족 + NMPC용 해석적 그래디언트 제공
- **실하드웨어 NMPC 검증**: 47.7 Hz 제어 주파수로 실시간 다자유도 NMPC 최초 실증

## Methods

| 구성요소 | 내용 |
|---------|------|
| FP 모델 | Euler-Lagrange 방정식 기반 제1원리 모델 (진실값 기준) |
| PINC | 입력과 초기 조건을 받는 PINN; implicit differentiation으로 NMPC 그래디언트 계산 |
| DD-PINN | 앤사츠 함수 구조로 초기 조건 만족 보장; 해석적 시간 미분 → 빠른 NMPC |
| GRU-RNN | 최적 HPO 완료 RNN (비교군, 실제 데이터 없이 FP 데이터로 학습) |
| HPO | ASHA 알고리즘으로 모든 모델 공정 비교 |
| NMPC | CasADi 기반, IPOPT 솔버, horizon 5스텝 |
| 플랫폼 | PyTorch, dual RTX 3080 Ti (학습), ARM Cortex-A55 (실시간) |

**도메인 변수 δ**: 부하 질량 (0 g, 100 g) × 기저부 방향 (6방향) = 12개 도메인. 훈련 시 1개 도메인, 나머지 11개는 일반화 평가.

## Key Results

| 지표 | 값 |
|------|-----|
| DD-PINN 추론 속도 | **2 μs** (vs. Euler 932 μs: **467배 빠름**, RK4 754 μs: 377배 빠름) |
| NMPC 제어 주파수 | **47.7 Hz** |
| PI 대비 오차 감소 | **평균 14.6%** (모든 실험 평균) |
| 도메인 일반화 | 1개 학습 도메인 → 12개 미지 도메인 성공 |
| DD-PINN 학습 시간 | 2.8일 (dual RTX 3080 Ti) |
| PINC 학습 시간 | 6일 |
| RNN vs DD-PINN | RNN이 추론 속도에서 미세하게 우세; 일반화는 DD-PINN이 압도적 우세 |

> [!note] RNN은 데이터 없이 FP 시뮬레이션 데이터로만 학습했음에도 빠른 추론 가능. 그러나 미지 도메인 일반화에서 DD-PINN이 월등.

## Limitations / Open Questions

- FP 모델 필요 — 완전 데이터 기반이 아님 (FP 모델로부터 collocation point 생성)
- 학습 시간이 2.8–6일로 긴 편 — 온라인 적응 학습 불가
- 3D 위치 제어만 검증; 힘/토크 제어 미적용
- 도메인 변수 δ를 사전에 알아야 함 (실시간 식별 아님)
- 실제 소프트 로봇 특정 적용; 다른 유형 시스템으로의 이전 일반성 미검증
- 참고문헌 [71]에 동일 그룹의 차량 동역학 PINN 논문(Zeipel et al., TechRxiv 2024)이 존재하나 미출판

## Research Ideas

### Idea 1: PINN 서로게이트 기반 EV 파워트레인 NMPC
DD-PINN 프레임워크를 EV 파워트레인(배터리-모터-섀시 결합 동역학)에 적용. FP 모델 없이 실험 데이터로 PINN 학습 후, 기존 선형 MPC 대비 비선형 NMPC를 수십 Hz로 실행.
→ [[pinn-surrogate-ev-nmpc]]

### Idea 2: 가변 부하 조건 EV 섀시 제어를 위한 도메인 일반화 PINN
δ 변수를 차량 하중(승객 수, 화물 무게), 노면 조건 등으로 해석. 다양한 부하 조건을 δ로 파라미터화하고, 소수의 조건에서 학습한 PINN을 미지 부하 조건에 일반화.
→ [[adaptive-partitioning-ev-chassis]]와 결합 가능

### Idea 3: Physics-Informed 차량 상태 추정 (FP → NN 가속)
PINN 앤사츠 구조를 EKF/UKF의 상태 전이 예측 단계 가속에 활용. 비선형 차량 동역학 적분을 PINN으로 대체해 추정기 계산 비용 절감.

## Connections

- [[schafke-2026-virtual-wheel-speed-sensor]] — 동일 연구그룹 (Simon Ehlers 공저자, Leibniz Hannover iMeS); 차량 동역학 측 응용
- [[zhang-2026-koopman-mpc-time-delayed]] — 같은 문제 구조 (비선형 시스템의 학습 기반 서로게이트로 MPC 가속); Koopman vs PINN 방법론 비교 관심
- [[riccardi-2026-noncentralized-mpc-partitioning]] — 분산 MPC와의 결합: PINN 서로게이트 + 파티셔닝 방법론
- [[pinn-surrogate-ev-nmpc]] — 이 논문에서 파생된 EV 적용 연구 아이디어
- [[physics-informed-neural-networks]] — 핵심 방법론 개념 페이지
- [[leibniz-imes-group]] — 저자 소속 연구그룹 페이지

> [!note] 참고문헌 [71]: Zeipel, Habich, Seel, Ehlers, "Fast and accurate prediction of vehicle dynamics using physics-informed neural networks," TechRxiv, 2024. 동일 그룹의 차량 동역학 PINN 논문 — ingest 우선순위 높음.

## Notable Quotes / Figures

> "To the best of our knowledge, this is the first work to use PINNs for a multi-DoF soft robot." — Introduction

> "The DD-PINN is 467 times faster than Euler integration, enabling 47.7 Hz NMPC on embedded hardware." — Results

**Figure 3**: PINC vs DD-PINN 아키텍처 비교 — DD-PINN의 앤사츠 구조가 초기 조건 만족과 해석적 그래디언트를 동시에 제공함을 도식화.

**Figure 6**: 12개 도메인에서의 일반화 성능 — 부하 0g/100g × 6방향 조합. DD-PINN이 RNN 대비 일관된 일반화 우위.
