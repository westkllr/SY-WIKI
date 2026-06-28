---
title: "전동화 차량 통합 섀시 제어를 위한 적응형 분산 MPC 파티셔닝"
type: research-idea
status: raw
tags: [MPC, EV, chassis-control, distributed-control, partitioning, adaptive-control, PINN]
inspired_by: [riccardi-2026-noncentralized-mpc-partitioning, habich-2026-pinn-mpc-soft-robot]
last_updated: 2026-06-24
---

## One-line pitch

EV의 운전 모드 전환(EV/HEV/회생제동)에 따라 서브시스템 결합 구조가 변하는 점을 이용해, 예측 파티셔닝으로 분산 MPC 구조를 실시간 재구성하는 통합 섀시 제어기.

## Background

기존 EV/HEV 통합 섀시 제어(구동력 + 제동력 + 조향)는 파티션을 설계 시점에 고정 결정 (사실상 휴리스틱 파티셔닝). 하지만 EV는 운전 모드에 따라 서브시스템 간 결합이 극적으로 변한다:
- 순수 전기 주행: 모터-배터리 결합 강함, 변속기 분리
- 회생제동: 모터-휠-배터리 결합 구조 변경
- 긴급 제동(emABS): 모든 서브시스템 타이트한 결합 필요

[[riccardi-2026-noncentralized-mpc-partitioning]]은 "예측 파티셔닝" 개념을 제안했으나 차량 응용은 없음. 논문 자체가 교통 분야의 파티셔닝이 "현저히 부족"하다고 명시.

## Proposed approach

1. **오프라인 단계**: 주요 운전 모드별 최적 파티션을 MIP 공식화로 사전 계산 (모드 수는 유한하므로 실용적)
2. **온라인 단계**: 모드 전환 예측(MPC 예측 호라이즌 내)을 이용해 파티션 전환 타이밍 결정
3. **전환 관리**: 파티션 전환 시 제어기 초기화 및 연속성 보장 방법 연구

## Why this is feasible

- EV 운전 모드 수는 유한 (3-5개) → MIP가 현실적
- 교수님의 emABS, 회생제동, HEV 제어 기존 연구가 서브시스템 모델 제공
- Hyundai 협력: 실차 검증 환경 가능성
- [[riccardi-2026-noncentralized-mpc-partitioning]]의 멀티-토폴로지 표현이 이론적 토대

## Novelty

- 기존 EV 섀시 제어: 파티셔닝 고정
- 기존 파티셔닝 연구: 교통 분야 적용 없음, 특히 EV 결합 구조 변화 다룬 연구 없음
- 이 연구의 새로운 점: "EV 운전 모드 = 토폴로지 변화"를 명시적으로 모델링 → 적응형 파티셔닝

## Open questions

- 파티션 전환 시 안정성 보장 (Lyapunov 또는 ISS 분석 필요)
- 예측 호라이즌 내 모드 전환 예측 정확도가 파티셔닝에 미치는 영향
- 실시간 파티션 전환의 계산 부담 (임베디드 ECU 구현 가능성)

## 연관 아이디어 업데이트 (2026-06-24)

[[habich-2026-pinn-mpc-soft-robot]]의 DD-PINN이 서브시스템 FP 모델을 467× 가속한다는 결과는 이 아이디어의 실시간 실현 가능성을 높임: **각 파티션 서브시스템의 내부 모델을 DD-PINN으로 대체**하면 분산 NMPC의 계산 병목 해소 가능. [[pinn-surrogate-ev-nmpc]]와 결합 고려.
