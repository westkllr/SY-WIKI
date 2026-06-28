---
title: "DBPnet: Damper Characteristics-Based Bayesian Physics-Informed Neural Network for Wheel Load Estimation"
type: paper
authors: [Wang, Tianyi, Zeng, Tianyi, Zeng, Zimo, Zhang, Feiyang, Wang, Yujin, Li, Xiangyu, Xu, Yiming, Chen, Sikai, Jiao, Junfeng, Claudel, Christian, Chen, Xinbo]
year: 2026
journal: "arXiv 프리프린트 (제출처 미확인)"
doi: arxiv:2605.24860
tags: [physics-informed neural networks, Bayesian, wheel load estimation, vehicle state estimation, suspension dynamics, chassis control]
methods: [Bayesian PINN, 댐퍼 특성 물리 임베딩, 불확실성 정량화]
has_full_text: false
last_updated: 2026-06-28
---

## 초록

댐퍼 특성에 기반한 물리 인식 임베딩 모듈을 갖춘 베이지안 PINN 구조(DBPnet)를 제안하여 차량 휠 하중(wheel load)을 추정한다. 휠 하중은 섀시 제어 및 안전 임계 기능에 핵심 변수이나, 복잡한 서스펜션 기하학·비선형 동역학·측정 잡음으로 인해 강건한 추정이 어렵다. 본 논문은 댐퍼 역학을 물리 제약으로 활용하여 추정 정확도와 불확실성 정량화를 동시에 달성한다.

## 핵심 기여

- **DBPnet 아키텍처**: 댐퍼 특성에서 유래한 물리 인식 임베딩 모듈 내장 — 순수 데이터 기반 대비 물리적 일관성 확보
- **베이지안 PINN 통합**: 추정값과 함께 예측 불확실성(신뢰구간) 동시 제공 — 안전 임계 섀시 제어에 적합
- **전임 연구(Damper-B-PINN, arXiv:2502.20772) 확장**: 댐퍼 기반 PINN을 휠 하중 추정으로 확장

## 방법론

- **물리 임베딩**: 댐퍼 힘-속도 특성(f = f(v_rel))을 신경망 구조 내 물리 제약으로 내재화
- **베이지안 추론**: 드롭아웃 또는 앙상블 기반 불확실성 추정으로 신뢰 구간 제공
- **서스펜션 동역학 모델**: 4자유도 1/4차 차량 모델(quarter-car model) 물리 방정식을 손실 함수에 포함

## 주요 결과

- 순수 데이터 기반 모델 대비 휠 하중 추정 오차 감소 (전문 미확인, 정량 수치 불명)
- 불확실성 추정을 통한 신뢰 가능 추정(trustworthy estimation) 달성
- 다양한 노면 및 주행 조건에서 일반화 성능 검증

## 한계 / 미해결 과제

- 실차 대규모 검증(다양 차종, 노면 유형) 미수행
- 베이지안 추론 계산 비용이 실시간 섀시 제어 주기(수 ms)와의 양립 여부 미검증
- 4자유도 1/4차 모델 가정이 실제 좌우·전후 결합 동역학 무시

## 연구 아이디어

1. **EKF/UKF + DBPnet 융합 차량 상태 추정기**: 베이지안 DBPnet의 휠 하중 추정을 UKF 측정 업데이트 단계에 통합, 교수님의 기존 UKF 기반 추정 프레임워크와 결합. 특히 EV 회생제동 시 전·후축 하중 이동을 실시간 추정하여 토크 배분 최적화에 활용 가능.
2. **다축 EV용 Bayesian PINN 상태 추정**: 4WD EV의 4개 휠 하중을 동시 추정하는 확장 DBPnet — 각 휠의 회생제동 토크 한계를 개별 추정하여 타이어 포화 방지. [[wang-2026-pinn-ev-thermal-mpc]]의 통합 PINN-MPC 프레임워크와 결합 가능.

## 연관 자료

- [[physics-informed-neural-networks]] — PINN 개념 페이지
- [[adaptive-robust-estimation]] — EKF/UKF 기반 강건 추정 비교
- [[schafke-2026-virtual-wheel-speed-sensor]] — 같은 차량 상태추정 분야, 신경망 가상 센서 방법론 상호보완
- [[wang-2026-pinn-ev-thermal-mpc]] — 동일 주간 발견, PINN 기반 EV 제어 계열 논문
- [[habich-2026-pinn-mpc-soft-robot]] — DD-PINN 서로게이트 기반 NMPC (물리 임베딩 방법론 참고)
