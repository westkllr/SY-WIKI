---
title: "비중앙화 MPC (Non-Centralized MPC)"
type: concept
tags: [MPC, distributed-control, large-scale-systems, optimization]
papers: [riccardi-2026-noncentralized-mpc-partitioning]
last_updated: 2026-06-21
---

## 개요

비중앙화 MPC(NCen-MPC)는 대규모 시스템을 여러 서브시스템으로 분해하고, 각각에 독립적인 MPC 제어기를 할당하는 제어 구조. 단일 중앙 MPC가 계산 부담이나 통신 지연 때문에 실용적이지 않을 때 사용.

## NCen-MPC 유형

| 유형 | 서브시스템 간 통신 | 파티션 변경 | 주요 특징 |
|------|------------------|------------|----------|
| **Dec-MPC** (분권화) | 없음 | 고정 | 완전 독립; 최단순 구조 |
| **DMPC** (분산) | 있음 (반복 협상) | 고정 | 성능 최적에 가까우나 통신 부담 |
| **HMPC** (계층형) | 상하 계층 간 | 고정 | 상위 = 느린 글로벌 최적화, 하위 = 빠른 로컬 제어 |
| **Coal-MPC** (연합형) | 동적 | 동적 변경 | 토폴로지 변화에 가장 유연 |

## 핵심 개념: 파티셔닝

어떤 NCen-MPC를 선택하든, 시스템을 어떻게 서브시스템으로 분할할지(파티셔닝)가 성능을 좌우. 파티셔닝은 주로 시스템의 결합 그래프(coupling graph)를 분석해 결정. → 자세한 내용: [[graph-partitioning-control]]

## 차량 제어와의 연관성

- **통합 섀시 제어**: 구동력, 제동력, 조향을 독립 MPC로 분리 → HMPC 구조
- **에너지 관리**: 배터리-모터-재생제동 간 최적화 → DMPC 구조  
- **차량 군집(Platoon)**: 각 차량이 독립 MPC, 앞뒤 차량과 정보 공유 → DMPC 구조
- **EV 다중 모터**: 모드 변환 시 결합 구조 변경 → Coal-MPC 또는 적응형 파티셔닝 필요

## 관련 문헌

- [[riccardi-2026-noncentralized-mpc-partitioning]] — NCen-MPC 파티셔닝 체계적 서베이 (Annual Reviews in Control, 2026)
