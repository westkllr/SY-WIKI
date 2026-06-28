---
title: "Physics-informed Deep Mixture-of-Koopmans Vehicle Dynamics Model with Dual-branch Encoder for Distributed Electric-drive Trucks"
type: paper
authors: [Miao, Jinyu, Zhang, Pu, Yan, Rujun, He, Yifei, Zhang, Bowei, Fu, Zheng, Wang, Ke, Song, Qi, Jiang, Kun, Yang, Mengmeng, Yang, Diange]
year: 2026
journal: "arXiv 프리프린트 (제출처 미확인)"
doi: arxiv:2603.17416
tags: [Koopman operator, physics-informed, vehicle dynamics, electric-drive trucks, autonomous driving, data-driven, mixture model]
methods: [Koopman 연산자, 물리 정보 감독, Mixture-of-Koopman, 쌍분기 인코더, EDMD, 재귀 부분공간 식별]
has_full_text: false
last_updated: 2026-06-28
---

## 초록

분산 전동 구동 트럭(DET: Distributed Electric-drive Truck)의 복잡한 비선형 동역학을 위해 Koopman 연산자 이론을 활용한 완전 데이터 기반 동역학 모델링 방법을 제안한다. Koopman 연산자를 Mixture-of-Experts 구조로 확장하여 다양한 주행 패턴을 수용하고, 시간적 차량 운동의 기하학적 일관성을 물리 감독 메커니즘으로 학습 과정에 통합한다. TruckSim 고충실도 시뮬레이션 및 실차 실험에서 최첨단 장기 상태 추정 성능을 달성한다.

## 핵심 기여

- **Mixture-of-Koopmans 프레임워크**: 단일 Koopman 연산자를 혼합 전문가(MoE) 구조로 확장 — DET의 다양한 주행 패턴(고속/저속, 직진/곡선, 적재/공차)을 단일 선형 표현으로 통합
- **물리 정보 감독 메커니즘**: 시간적 차량 운동의 기하학적 일관성(geometric consistency of temporal vehicle motion)을 학습 손실에 통합 — 물리 법칙 위반 없이 데이터 기반 학습
- **쌍분기 인코더(Dual-branch Encoder)**: Koopman 기반 방법(KODE)의 기저(basis)를 제공하는 특화 아키텍처 — 동역학 모드 분해 효율화
- **재귀 부분공간 식별**: 대규모 시뮬레이션 데이터로부터 Koopman 연산자를 효율적으로 학습

## 방법론

- **Koopman 연산자 이론**: 비선형 동역학 x_{k+1} = f(x_k)를 고차원 리프팅(lifting) 공간에서 선형 시스템 z_{k+1} = Kz_k로 표현
- **EDMD(Extended Dynamic Mode Decomposition)**: 관측 함수(observable)로 비선형 시스템의 Koopman 행렬 K를 학습
- **물리 감독**: 차량의 기하학적 운동 일관성(연속 프레임 간 좌표 변환 일관성)을 손실 함수에 추가
- **TruckSim + 실차**: 고충실도 시뮬레이터와 실제 DET로 이중 검증

## 주요 결과

- 장기(long-term) 동역학 상태 추정에서 최첨단(SOTA) 성능 달성
- 기존 단일 Koopman 대비 다양한 주행 패턴 일반화 능력 향상
- 선형 제어 전략(MPC 등)과의 호환성: Koopman 리프팅 공간에서 LQR/MPC 직접 적용 가능

## 한계 / 미해결 과제

- DET(대형 트럭) 특화 설계 — 일반 승용 EV로의 이전성 미검증
- Koopman 리프팅 차원이 커질수록 계산 비용 증가: 실시간 MPC 구현 가능 차원 한계 존재
- 타이어 포화·극한 기동 조건에서의 Koopman 선형화 오차 미분석

## 연구 아이디어

1. **승용 EV 섀시 Mixture-of-Koopman MPC**: 본 논문의 MoK-DET 프레임워크를 일반 승용 EV(단일 또는 인휠 모터)의 횡-종방향 통합 동역학 모델링에 적용, 각 주행 시나리오(도심/고속도로/곡선 급기동)별 Koopman 서브모델을 자동 선택하는 스위칭 MPC 연구. [[zhang-2026-koopman-mpc-time-delayed]]의 시간지연 Koopman MPC와 결합 가능.
2. **물리 감독 Koopman + EKF 융합 상태 추정기**: Miao et al.의 물리 감독 Koopman 모델을 EKF의 예측 모델로 활용, 전통적 물리 기반 차량 모델 대체. 교수님의 EKF/UKF 상태추정 연구 영역(Area 5)에서 "Koopman 리프팅 공간 EKF"로 비선형성 처리 능력 향상. 특히 DET의 토크 벡터링 제어에 적합.

## 연관 자료

- [[zhang-2026-koopman-mpc-time-delayed]] — Koopman MPC (시간지연 비선형 시스템, 동일 계열)
- [[koopman-operator-control]] — Koopman 연산자 개념 페이지
- [[physics-informed-neural-networks]] — PINN 개념 (물리 정보 감독 메커니즘 공유)
- [[loya-2026-koopman-offroad-vehicle]] — Koopman 오프로드 차량 제어 (동일 주간 발견)
- [[habich-2026-pinn-mpc-soft-robot]] — 물리 기반 신경망 MPC 선례

## 주목할 인용

> "A novel dual-branch encoder is proposed which provides a basis for the Koopman-based methods (KODE), and a physics-informed supervision mechanism, grounded in geometric consistency of temporal vehicle motion, is incorporated into the training process." (Miao et al., 2026)
