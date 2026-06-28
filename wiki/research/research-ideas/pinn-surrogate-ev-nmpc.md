---
title: "PINN 서로게이트 기반 EV 파워트레인·섀시 NMPC"
type: research-idea
status: developing
tags: [PINN, NMPC, EV, surrogate model, powertrain, chassis control, domain generalization]
inspired_by: [habich-2026-pinn-mpc-soft-robot, zhang-2026-koopman-mpc-time-delayed]
last_updated: 2026-06-24
---

## One-line pitch

DD-PINN 서로게이트 모델로 EV 비선형 동역학을 μs 수준 예측하여 실시간 NMPC를 실현한다.

## Background

EV 파워트레인·섀시의 비선형 동역학(배터리 열역학, 전동기-휠 결합 토크, 타이어 슬립)은 제1원리 모델로 ms 이상 걸려 고주파 MPC(> 50 Hz)에서 병목. 현재 실용화 MPC는 선형화 모델에 의존하며, 비선형 거동이 큰 고속 과도구간·슬리퍼리 노면에서 성능 열화.

[[habich-2026-pinn-mpc-soft-robot]]은 DD-PINN이 제1원리 모델 대비 467배 빠른 추론으로 47 Hz NMPC를 달성함을 실증. 동일 Leibniz Hannover 그룹은 차량 동역학 PINN 논문(Zeipel et al., TechRxiv 2024)도 투고한 상태. 방법론이 EV 시스템으로 이전 가능한 성숙도에 있음.

## Proposed Approach

1. **FP 모델 확보**: EV 배터리-모터-타이어 결합 동역학의 제1원리 시뮬레이터 구축 (기존 Simulink 모델 재활용 가능)
2. **DD-PINN 학습**: collocation point를 FP 시뮬레이션에서 생성; 앤사츠 구조로 초기 조건 자동 만족
3. **도메인 변수 δ 정의**: 차량 하중(공차/적재), 노면 마찰계수(μ), SOC 구간 등을 δ로 파라미터화
4. **NMPC 통합**: CasADi + IPOPT로 DD-PINN 서로게이트 기반 NMPC 구현; 100 Hz 이상 목표
5. **실험 검증**: HIL(Hardware-in-the-Loop) 또는 차량 실험으로 기존 선형 MPC 대비 성능 비교

## Why This Is Feasible

- DD-PINN 코드 및 CasADi NMPC 파이프라인이 [[habich-2026-pinn-mpc-soft-robot]]에서 검증됨
- 차량 동역학 PINN 사례: Zeipel et al. (2024) — 동일 그룹이 차량에 먼저 시도
- 연구실 보유 EV 실험 데이터 및 시뮬레이터 활용 가능
- [[zhang-2026-koopman-mpc-time-delayed]]의 Koopman MPC와 비교 연구로 논문 차별화 가능

## Novelty

- 기존 EV MPC는 선형화 or Koopman 선형화 모델 기반; **물리 법칙을 내재화한 비선형 서로게이트 NMPC**는 미개척
- 도메인 변수 δ로 다양한 하중·노면 조건에 단일 모델로 대응 — 기존 gain-scheduling 또는 adaptive MPC와 차별
- 계산 비용 절감(467× 이상)이 실용화 장벽 해소 — 논문의 실용적 기여 명확

## Open Questions

- EV 동역학은 소프트 로봇보다 입력 차원(u: 토크, 조향)과 상태 차원(x: 속도, 슬립, SOC, 온도)이 훨씬 크다 — 고차원에서 DD-PINN 성능 유지 여부
- δ 변수 온라인 식별 방법 — 논문에서는 δ를 사전 알고 있음; 실차에서는 추정 필요
- 학습 시간(2.8일+)이 모델 업데이트 주기와 맞지 않을 경우 대응 방안
- Safety constraint 처리: NMPC의 안전 제약을 DD-PINN 기반에서 어떻게 보장할지
