---
title: "Robust Koopman MPC with Sets Updates for Time Delayed Systems"
type: paper
authors: [Zhang, Xinglong, Yao, Xinxin, Xu, Xin, You, Keyou, Hu, Dewen]
year: 2026
journal: arXiv preprint
doi: arxiv:2606.16485
tags: [Koopman-operator, MPC, robust-control, time-delay, uncertainty-sets, nonlinear-systems, adaptive-MPC, data-driven-control]
methods: [Koopman MPC, Robust Adaptive MPC, Online Uncertainty Set Updates, Positively Invariant Sets, Lifted Observable Space]
has_full_text: false
last_updated: 2026-06-23
---

## Abstract

Koopman operator-based linear MPC on a lifted observable space has emerged as a promising framework for controlling nonlinear systems, with recent work addressing robust design under modeling errors. However, existing robust Koopman MPC designs rely on pre-estimated, fixed uncertainty sets — which is conservative because the actual uncertainty is state-and-control-dependent and time-varying. Furthermore, no prior work addresses closed-loop robustness for nonlinear systems with time delays. This paper presents a robust adaptive Koopman MPC approach that performs online updates of uncertainty sets for a class of nonlinear time-delayed systems, reducing conservatism while maintaining rigorous robust guarantees.

## Key Contributions

- **First Koopman MPC design for nonlinear time-delayed systems**: Explicitly addresses closed-loop robustness with time delays — a significant gap in prior literature.
- **Online uncertainty set updates**: Eliminates the conservatism of fixed, pre-calculated uncertainty bounds by adapting the sets based on current state and control.
- **Adaptive robust invariant sets**: Derives robust positively invariant (RPI) sets compatible with the online-updated uncertainty model.
- **Unified framework**: Bridges Koopman operator theory, robust MPC, and time-delay systems in a single formulation.
- **Affiliations**: National University of Defense Technology (NUDT) + Tsinghua University — high-impact Chinese control theory groups.

## Methods

- **Koopman lifting**: Maps nonlinear state-space into a high-dimensional linear observable space; enables linear MPC formulation for inherently nonlinear dynamics.
- **Robust Koopman MPC**: Formulates tube-based or min-max MPC on the lifted space with uncertainty bounding.
- **Online uncertainty set updates**: Real-time estimation of modeling error bounds as a function of current state/control trajectory; replaces static pre-computed sets.
- **Robust Positively Invariant (RPI) sets**: Recomputed online to ensure constraint satisfaction under the updated uncertainty model.
- **Time-delay handling**: Extended Koopman lifting that incorporates delayed states/inputs into the observable basis.

## Key Results

- Demonstrates reduced conservatism vs. fixed-set Koopman MPC (quantitative results not retrieved in search abstract).
- Closed-loop stability and constraint satisfaction guaranteed for the proposed class of time-delayed nonlinear systems.
- Online computational burden not explicitly quantified in the retrieved summary.

## Limitations / Open Questions

- Restricted to a specific class of nonlinear time-delayed systems; generality to arbitrary delay structures (distributed, state-dependent delays) unproven.
- Koopman lifting quality depends heavily on basis function selection; systematic basis design for vehicle dynamics is an open problem.
- Online uncertainty set updates may introduce latency — real-time feasibility for fast vehicle dynamics (10–100 Hz control loops) not demonstrated.
- No vehicle-specific application reported; transferability to powertrain or chassis control requires validation.

## Research Ideas

1. **Koopman MPC for electrified powertrain with communication delays**: Apply this robust time-delay Koopman MPC to HEV/EV powertrain control where CAN bus communication introduces measurable delays between sensor readings and actuator commands. The framework directly addresses this practical challenge and connects to [[optimal-control-electrified-powertrain]] and [[noncentralized-mpc]].

2. **Data-driven Koopman basis selection for vehicle lateral dynamics**: Use EDMD (Extended DMD) with vehicle-specific basis functions (tire slip angle, yaw rate products) to build a Koopman model for lateral dynamics, then deploy the robust adaptive MPC from this paper for real-time vehicle stability control with bounded slip angle. This bridges Koopman theory and [[safety-dynamics-electrified-vehicles]].

## Connections

- [[noncentralized-mpc]] — Koopman MPC could be distributed across chassis subsystems using the partitioning framework from [[riccardi-2026-noncentralized-mpc-partitioning]].
- [[adaptive-partitioning-ev-chassis]] — Research idea; Koopman lifting + adaptive partitioning for EV chassis is now more feasible with this paper.
- [[data-driven-partitioning-energy-management]] — Data-driven Koopman for energy management could extend this paper's framework.
- [[koopman-operator-control]] — 핵심 방법론 개념 페이지 (기존 MPC와 비교, EDMD, 적용 조건 포함).
- Connects to theme of [[vehicle-state-estimation]] — Koopman state estimation via lifted observables is a natural extension.

## Notable Quotes / Figures

> "Deriving a robust positively invariant set using a precalculated uncertainty set can be conservative because the uncertainty set bound is time-varying and dependent on the state and control." — from abstract
