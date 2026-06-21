---
title: "데이터 기반 파티셔닝을 이용한 EV 에너지 관리 분산 MPC"
type: research-idea
status: raw
tags: [MPC, EV, energy-management, data-driven, machine-learning, partitioning]
inspired_by: [riccardi-2026-noncentralized-mpc-partitioning]
last_updated: 2026-06-21
---

## One-line pitch

실주행 데이터에서 EV 에너지 관리 서브시스템 간 실제 결합 강도(coupling strength)를 학습하고, 주행 패턴별 최적 분산 MPC 파티션을 자동 결정하는 데이터 기반 방법론.

## Background

EV 에너지 관리는 배터리 SOC 제어, 모터 토크 분배, 회생제동, (HEV의 경우) 엔진-모터 분배를 포함한 다중 서브시스템 최적화 문제. 현재 접근은:
- 단일 중앙 MPC: 계산 부담 큼
- 파티셔닝은 엔지니어가 직관으로 결정 (휴리스틱)

[[riccardi-2026-noncentralized-mpc-partitioning]]이 명시한 두 가지 공백을 동시에 타겟:
1. "데이터 기반 파티셔닝이 거의 연구되지 않음"
2. "에너지 관리에서의 파티셔닝 연구 부족"

## Proposed approach

1. **데이터 수집**: 다양한 주행 사이클(도심/고속도로/혼합)에서 서브시스템 간 정보 흐름 측정
2. **결합 강도 추정**: Granger causality 또는 mutual information으로 서브시스템 간 실제 결합 정량화 → 데이터 기반 결합 그래프 생성
3. **파티션 학습**: 주행 패턴 클러스터별 최적 파티션 사전 학습 (spectral clustering 또는 최적화 기반)
4. **온라인 적용**: 주행 패턴 실시간 분류 → 해당 파티션의 분산 MPC 활성화

## Why this is feasible

- 교수님 그룹의 에너지 관리 MPC 연구 기존 결과 활용 가능
- Hyundai 실주행 데이터 접근 가능성
- Granger causality/mutual information은 시계열 데이터에 직접 적용 가능한 성숙한 방법
- 주행 패턴 분류 자체는 기존 연구 활발 → 출발점 명확

## Novelty

- 기존 에너지 관리: 파티셔닝을 사람이 결정
- 기존 파티셔닝: 수식 모델 기반 (데이터 없음)
- 이 연구: 실주행 데이터로 결합 구조를 **발견**하고 파티션 자동 결정
- PINN 또는 차량 모델과 결합 시 "물리 정보 기반 데이터 파티셔닝"으로 확장 가능

## Open questions

- 결합 강도를 데이터에서 얼마나 정확하게 추정할 수 있는가
- 학습된 파티션이 분포 외(out-of-distribution) 주행 조건에서 얼마나 강인한가
- 주행 패턴 전환 시 파티션 전환의 과도 응답 처리
- [[adaptive-partitioning-ev-chassis]]와의 통합 가능성 (섀시 + 에너지 관리 통합 파티셔닝)
