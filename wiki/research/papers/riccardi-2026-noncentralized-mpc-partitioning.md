---
title: "Partitioning techniques for non-centralized predictive control: A systematic review and novel theoretical insights"
type: paper
authors: [Riccardi, Alessandro, Laurenti, Luca, De Schutter, Bart]
year: 2026
journal: Annual Reviews in Control
doi: 10.1016/j.arcontrol.2026.101046
tags: [MPC, distributed-control, decentralized-control, hierarchical-control, graph-partitioning, large-scale-systems, survey]
methods: [NCen-MPC, DMPC, Dec-MPC, HMPC, Coal-MPC, MIP, community-detection]
source_file: raw/papers/2026ARC_Riccardi.pdf
has_full_text: true
last_updated: 2026-06-21
---

## Abstract

TU Delft의 Riccardi, Laurenti, De Schutter가 작성한 비중앙화 MPC(NCen-MPC)의 파티셔닝 기법에 대한 체계적 서베이. 분산(DMPC), 분권화(Dec-MPC), 계층적(HMPC), 연합(Coal-MPC) 등 NCen-MPC 유형별 파티셔닝 기법을 5개 클래스로 분류하고, 최적 파티셔닝의 MIP 공식화와 "예측 파티셔닝(predictive partitioning)"이라는 새 개념을 제안한다. 전력망, 수자원, 풍력단지, 화학공정, 교통 등 다양한 응용 분야에 걸친 148편 이상의 논문을 분석한다.

## Key Contributions

- **5개 파티셔닝 클래스 분류**: 최적화 기반, 알고리즘 기반, 커뮤니티 탐지 기반, 게임이론 기반, 휴리스틱 기반
- **멀티-토폴로지 표현(multi-topological representations)**: 시스템 결합(coupling)의 다양한 측면을 동시에 나타내는 프레임워크 제안 — 상태, 입력, 제약의 결합을 별도 그래프로 표현
- **MIP 공식화**: 최적 파티셔닝 문제를 Mixed Integer Program으로 형식화 (계산 복잡도는 높지만 이론적 기준점 제공)
- **"예측 파티셔닝(predictive partitioning)"** 개념 최초 제안: MPC 예측 호라이즌 내에서 토폴로지 변화를 예측하여 사전에 파티션을 조정하는 개념 (현재 미해결 문제)
- **핵심 발견**: 모듈라리티 최대화(modularity maximization) ≠ 최적 제어 성능. 파티션 품질은 반드시 시뮬레이션으로 검증해야 함

## Methods

### NCen-MPC 유형 분류

| 유형 | 풀네임 | 특징 |
|------|--------|------|
| Dec-MPC | Decentralized MPC | 서브시스템 간 통신 없음, 완전 독립 |
| DMPC | Distributed MPC | 서브시스템 간 정보 공유, 반복 협상 |
| HMPC | Hierarchical MPC | 상위/하위 제어기 계층 구조 |
| Coal-MPC | Coalitional MPC | 동적으로 협력 집단(coalition) 변경 |

### 5개 파티셔닝 클래스

1. **최적화 기반**: 목적함수(제어 성능) 직접 최적화. 가장 이론적으로 정확하지만 계산 부담 큼. MIP 공식화 포함.
2. **알고리즘 기반**: Spectral clustering, Recursive Bisection 등 그래프 분할 알고리즘. 빠르지만 제어 성능 보장 없음.
3. **커뮤니티 탐지 기반**: 모듈라리티 최대화 등 네트워크 과학의 커뮤니티 탐지 알고리즘 활용. 대형 네트워크에 강하지만 제어 성능과의 상관관계 불명확.
4. **게임이론 기반**: 서브시스템을 플레이어로 모델링, 파티셔닝을 내쉬 균형(Nash equilibrium) 문제로 형식화. Coal-MPC에 특히 적합.
5. **휴리스틱 기반**: 물리적 또는 엔지니어링 직관으로 파티션 결정. 계산 부담 최소이나 최적성 보장 없음.

## Key Results

- 5개 클래스 모두 각각의 적용 상황이 있으며, 단일 "최고의 기법"은 존재하지 않음
- 표준화된 벤치마크 부재로 기법 간 객관적 비교가 불가능한 것이 현 분야의 핵심 문제
- 커뮤니티 탐지 기반 기법이 가장 많이 사용되지만 제어 성능과의 직접적 연관성이 가장 약함
- 교통/차량 응용은 전력망·수자원 등 타 분야 대비 연구량이 현저히 부족 (차량 군집주행 관련 Liu et al. 2019, Maxim & Caruntu 2022 등 소수)

## Limitations / Open Questions

- **시간 변화 파티셔닝(time-varying partitioning)**: 실시간으로 토폴로지가 변하는 시스템에 대한 방법론 미성숙
- **표준 벤치마크 부재**: 기법 간 객관적 성능 비교 불가능
- **데이터 기반 파티셔닝**: 머신러닝을 활용한 파티셔닝 연구 거의 없음
- **복원력/강인성**: 통신 장애나 서브시스템 고장에 대한 파티셔닝 강인성 미연구
- **예측 파티셔닝**: 개념 제안에 그침, 구체적 알고리즘 없음

## Research Ideas

### 아이디어 1: 전동화 차량의 적응형 분산 MPC 파티셔닝
- **배경**: 하이브리드 EV, 다중 모터 EV는 운전 모드(EV/HEV/재생제동)에 따라 서브시스템 간 결합(coupling) 구조가 변한다. 이는 이 논문의 "시간 변화 토폴로지" 문제의 직접적 사례.
- **아이디어**: EV 통합 섀시 제어(구동력/제동력/조향 통합)에 예측 파티셔닝을 적용. 주행 조건 변화를 예측해 사전에 DMPC 파티션을 재구성.
- **새로운 점**: 이 논문은 개념만 제안했고 차량에 적용한 사례는 없음.
- 관련: [[distributed-mpc-ev-chassis-control]] (아이디어 페이지)

### 아이디어 2: 데이터 기반 파티셔닝을 이용한 EV 에너지 관리
- **배경**: EV/HEV 에너지 관리는 배터리, 모터, 변속기, 회생제동 등 다중 서브시스템 최적화. 논문이 명시한 "데이터 기반 파티셔닝 미개척" 공백.
- **아이디어**: 실주행 데이터에서 서브시스템 간 실제 정보 흐름(coupling strength)을 학습, 주행 패턴별 최적 파티션을 오프라인 학습 후 온라인 적용.
- **새로운 점**: 기존 에너지 관리 연구는 파티셔닝을 설계자가 고정 결정. 데이터로 학습하는 접근 없음.
- 관련: [[data-driven-partitioning-energy-management]] (아이디어 페이지)

### 아이디어 3: 차량 군집주행의 동적 파티셔닝 (재생제동 협조 포함)
- **배경**: 차량 군집(platoon)은 대표적인 동적 토폴로지 시스템 (차량 가입/이탈). EV 군집의 경우 회생제동 협조 제어가 추가됨.
- **아이디어**: Coal-MPC 기반 동적 파티셔닝으로 EV 군집에서 에너지 회수 극대화 + 안전 거리 유지 통합 제어.
- **새로운 점**: 논문 내 차량 군집 파티셔닝 연구는 에너지 측면 없음.

## Connections

- [[noncentralized-mpc]] — 이 논문이 다루는 핵심 개념
- [[graph-partitioning-control]] — 파티셔닝 기법 상세
- [[riccardi-2026]] — 저자 Alessandro Riccardi
- [[de-schutter-bart]] — 저자 Bart De Schutter (TU Delft)
- [[distributed-mpc-ev-chassis-control]] — 파생 연구 아이디어
- [[data-driven-partitioning-energy-management]] — 파생 연구 아이디어

## Notable Quotes

> "The concept of predictive partitioning refers to the computation of the optimal partition based on predicted topology changes, rather than on the current one." (Section 11.1)

> "Community detection-based methods are by far the most commonly used in the NCen-MPC literature, but we show that maximizing modularity does not necessarily correspond to achieving the best control performance." (Section 1, Introduction)

> "There is a significant lack of standardized benchmarks to objectively compare partitioning methods, which hinders progress in the field." (Section 11.2)
