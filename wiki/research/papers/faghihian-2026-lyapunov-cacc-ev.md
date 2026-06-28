---
title: "An Energy-Efficient Lyapunov-Based Cooperative Adaptive Cruise Controller for Electric Vehicles"
type: paper
authors: [Faghihian, Hamed, Ansari Bonab, Parisa, Sargolzaei, Arman]
year: 2026
journal: "IEEE Conference Publication (11107788)"
doi: arxiv:2604.08689
tags: [cooperative adaptive cruise control, electric vehicle, Lyapunov stability, regenerative braking, energy efficiency, V2V communication, CACC]
methods: [Lyapunov 기반 제어, 3차 EV 동적 모델, CACC, 회생제동 통합]
has_full_text: false
last_updated: 2026-06-28
---

## 초록

커넥티드·자율주행 전기차(EV) 플랫폼에서 에너지 효율 향상을 목표로 Lyapunov 안정성 이론에 기반한 협력 적응형 크루즈 제어(CACC) 알고리즘을 제안한다. V2V(차량 간) 통신을 통한 실시간 협조로 교통 흐름·안전·에너지 효율을 동시 개선하며, 가속 및 회생제동 동역학을 통합한 3차 EV 모델을 실험 데이터로부터 도출한다.

## 핵심 기여

- **회생제동 내재화 CACC**: 기존 CACC가 무시했던 회생제동 동역학을 3차 EV 동적 모델에 통합 — EV 특성에 맞춘 에너지 효율 최적화
- **Lyapunov 안정성 보장**: 제안 제어기의 안정성을 수학적으로 증명 — 안전성과 에너지 효율의 동시 달성
- **실측 데이터 기반 모델**: 실험 데이터로부터 도출한 3차 EV 동적 모델 사용 — 물리 기반 + 데이터 기반 하이브리드 접근

## 방법론

- **3차 EV 동적 모델**: 위치-속도-가속도 상태 공간에 회생제동 토크 및 모터 동역학 추가
- **Lyapunov 기반 제어**: V(x) = xᵀPx 형태의 Lyapunov 함수로 오차 수렴 및 간격 유지 보장
- **CACC 프레임워크**: V2V 통신으로 선행 차량 정보(속도, 가속도) 실시간 수신, 협력 제어 실현

## 주요 결과

- 에너지 효율 개선: 기존 CACC 대비 회생제동 활용으로 에너지 소비 감소 (구체적 수치 전문 미확인)
- Lyapunov 안정성 이론에 의한 폐루프 안정성 수학적 증명
- IEEE 학술대회 발표(IEEE Conference Publication 11107788)로 동료 심사 완료

## 한계 / 미해결 과제

- V2V 통신 지연(latency) 및 패킷 손실에 대한 강건성 분석 부재
- 혼합 교통 환경(EV + ICE 차량 혼재 플래툰) 적용 미검토
- 타이어 포화 및 제동 한계 조건에서의 안전 보장 메커니즘 명시 안 됨
- 단일 선행 차량 추종 CACC에 한정 — 다차량 플래툰 확장 미수행

## 연구 아이디어

1. **회생제동 토크 한계 인식 Lyapunov-CACC**: 교수님의 타이어 힘 기반 회생제동 토크 제한 연구([[kim-2026-regenerative-braking]] 참조)와 결합, EV 안정성 유지 조건 하에서 에너지 최대 회수를 보장하는 Lyapunov 안정적 CACC 설계. 특히 고속/급制 시 휠 슬립 방지와 회생제동 양립 문제 해결.
2. **개인화 CACC with 운전자 모델 통합**: [[rachavelpula-2026-personalized-ev-energy]]의 BiLSTM 운전자 모델을 CACC 참조 속도 프로파일 생성에 통합, 운전자 행동 패턴을 반영한 개인화된 에너지 효율 최적 CACC 구현. 교수님의 적응형·개인화 제어 연구 영역(Area 2)과 직접 연계.

## 연관 자료

- [[rachavelpula-2026-personalized-ev-energy]] — 개인화 EV 에너지 추정 (운전자 모델 활용)
- [[he-2026-eco-driving-ev-multi-speed]] — EV 에코드라이빙 속도 최적화 (에너지 효율 분야 상호보완)
- [[vedula-2026-predictive-energy-hybrid-powertrain]] — 하이브리드 파워트레인 예측 에너지 관리
- [[koopman-operator-control]] — 비선형 차량 제어의 선형화 방법론 (Lyapunov 대안)
- [[adaptive-partitioning-ev-chassis]] — EV 섀시 분산 MPC 연구 아이디어 (CACC 확장 방향)
