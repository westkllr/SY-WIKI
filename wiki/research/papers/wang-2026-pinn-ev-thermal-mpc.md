---
title: "Physics-Informed Predictive Control for Integrated Electric-Vehicle Thermal Management: An Open, Real-Data-Anchored Benchmark"
type: paper
authors: [Wang, Yifan]
year: 2026
journal: "American Modelica & FMI Conference 2026 (제출)"
doi: arxiv:2606.22529
tags: [physics-informed neural networks, predictive control, thermal management, electric vehicle, MPC, benchmark]
methods: [PINN, MPC, 실데이터 벤치마크]
has_full_text: false
last_updated: 2026-06-28
---

## 초록

물리 정보 신경망(PINN)과 모델 예측 제어(MPC)를 결합하여 전기차 통합 열관리 시스템을 위한 예측 제어 프레임워크를 제안한다. 실측 데이터를 기반으로 한 오픈 벤치마크를 구축하여 PINN 기반 MPC의 성능을 검증하며, 7페이지 분량의 논문으로 American Modelica & FMI Conference 2026에 제출되었다.

## 핵심 기여

- 전기차 통합 열관리 시스템 대상 PINN 기반 예측 제어 프레임워크 제안
- 실측 데이터 기반(Real-Data-Anchored) 오픈 벤치마크 구축 — 재현 가능한 비교 플랫폼 제공
- 물리 법칙 내재화로 데이터 부족 환경에서도 신뢰성 있는 열 모델 학습 가능

## 방법론

- **PINN(물리 정보 신경망)**: 열역학 지배 방정식을 손실 함수에 내재화하여 물리적으로 일관된 열 모델 학습
- **MPC(모델 예측 제어)**: PINN 서로게이트를 예측 모델로 활용, 유한 예측 지평선 내 에너지 소비 최소화
- **실데이터 앵커링**: 실제 EV 열관리 데이터를 기반으로 모델 학습 및 벤치마크 평가

## 주요 결과

- PINN 기반 예측 제어가 기존 규칙 기반 제어 대비 열관리 에너지 효율 개선 (구체적 수치는 전문 미확인)
- 오픈 벤치마크 제공으로 후속 연구의 비교 기준선(baseline) 역할

## 한계 / 미해결 과제

- 단일 저자 논문(7쪽)으로 대규모 실차 검증 범위 제한적
- 열관리 서브시스템(배터리·캐빈·파워트레인) 간 완전 통합 여부 불명확
- 실시간 PINN 추론 속도가 MPC 제어 주기 요건(수십 ms)을 충족하는지 미검증

## 연구 아이디어

1. **EV 섀시·파워트레인·열관리 통합 PINN-NMPC**: 본 논문의 열관리 PINN-MPC를 [[pinn-surrogate-ev-nmpc]]의 섀시/파워트레인 NMPC와 통합, 에너지 소비·배터리 수명·주행 동역학을 동시 최적화하는 계층 제어 구조 연구. 특히 회생제동 시 열 발생과 토크 배분의 동시 최적화가 핵심 난제.
2. **DD-PINN 서로게이트 + 적응형 열 모델 온라인 업데이트**: Habich et al.(2026) [[habich-2026-pinn-mpc-soft-robot]] 의 DD-PINN 서로게이트 기법을 EV 열 모델에 적용, 주행 조건(속도·주변온도·충전율)에 따른 온라인 모델 업데이트 메커니즘 연구.

## 연관 자료

- [[habich-2026-pinn-mpc-soft-robot]] — DD-PINN 서로게이트 기반 NMPC (467× 가속, 동일 방법론)
- [[physics-informed-neural-networks]] — PINN 개념 페이지
- [[pinn-surrogate-ev-nmpc]] — PINN 서로게이트 EV NMPC 연구 아이디어
- [[vedula-2026-predictive-energy-hybrid-powertrain]] — 하이브리드 파워트레인 에너지 예측 관리
- [[lokur-2026-energy-optimal-thermal-bev]] — 히트펌프 BEV 열관리 NMPC (보완 연구)
