---
title: "제어 시스템의 그래프 파티셔닝"
type: concept
tags: [graph-theory, partitioning, NCen-MPC, network-analysis, community-detection]
papers: [riccardi-2026-noncentralized-mpc-partitioning]
last_updated: 2026-06-21
---

## 개요

대규모 제어 시스템에서 서브시스템 분할(파티셔닝)을 그래프 이론으로 공식화하는 방법론. 시스템 구성 요소를 노드(node), 구성 요소 간 물리적/정보적 결합을 엣지(edge)로 표현하고, 그래프를 분할해 비중앙화 제어 구조를 결정.

## 5개 파티셔닝 클래스 (Riccardi et al. 2026)

### 1. 최적화 기반 (Optimization-based)
- 제어 성능 목적함수를 직접 최적화
- MIP(Mixed Integer Programming)로 공식화 가능
- 장점: 이론적 최적성 보장 가능
- 단점: 계산 복잡도 높음 (대형 시스템에 비실용적)

### 2. 알고리즘 기반 (Algorithmic)
- Spectral clustering, Recursive Bisection, k-means on graph
- 장점: 빠른 계산
- 단점: 제어 성능과 직접 연결되지 않음

### 3. 커뮤니티 탐지 기반 (Community Detection-based)
- 모듈라리티(modularity) 최대화 등 네트워크 과학 알고리즘
- **핵심 주의**: 모듈라리티 최대 파티션 ≠ 제어 성능 최적 파티션 (Riccardi et al. 2026이 명시)
- 실용적이고 대형 네트워크에 강하나 성능 보장 없음

### 4. 게임이론 기반 (Game-theoretic)
- 서브시스템을 플레이어, 파티셔닝을 게임으로 모델링
- 내쉬 균형(Nash equilibrium)으로 안정적 파티션 도출
- Coal-MPC에 특히 적합

### 5. 휴리스틱 기반 (Heuristic)
- 물리적 직관 또는 엔지니어링 경험으로 결정
- 계산 부담 없음; 하지만 최적성 보장 없음
- 차량 제어의 전통적 분리 (파워트레인 / 섀시 / 조향)가 사실상 휴리스틱 파티셔닝

## 멀티-토폴로지 표현

실제 시스템은 상태 결합, 입력 결합, 제약 결합이 서로 다른 그래프 구조를 가짐. Riccardi et al. (2026)은 이를 동시에 표현하는 멀티-토폴로지 표현법을 제안.

예시 (EV): 배터리-모터 간 에너지 흐름(입력 결합)과 배터리-모터 간 온도 동역학(상태 결합)은 서로 다른 그래프.

## 핵심 미결 문제

- 표준 벤치마크 없음 → 기법 비교 어려움
- 시간 변화 토폴로지(동적 파티셔닝) 미해결
- 데이터 기반 파티셔닝 거의 미개척
- **예측 파티셔닝**: 미래 토폴로지 변화를 예측해 사전 대응 (개념만 제안됨)

## 관련 개념

- [[noncentralized-mpc]] — 파티셔닝이 필요한 제어 구조
- [[riccardi-2026-noncentralized-mpc-partitioning]] — 체계적 서베이
