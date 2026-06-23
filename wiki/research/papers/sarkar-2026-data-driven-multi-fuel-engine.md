---
title: "Data-driven Control with Real-time Uncertainty Compensation for Multi-Fuel Engines"
type: paper
authors: [Sarkar, Rajasree, Banerjee, Arunava, Raju, Sathya Aswath Govind, Altiner, Ishan Berk, Sun, Zongxuan, Kim, Kenneth, Kweon, Chol-Bum Mike]
year: 2026
journal: arXiv preprint
doi: arxiv:2606.16171
tags: [multi-fuel-engine, data-driven-control, Gaussian-process, uncertainty-compensation, combustion-control, powertrain, adaptive-control, GPR]
methods: [Gaussian Process Regression, Data-Driven Control, Uncertainty Compensation, Pseudo-Engine-Speed, Combustion Phasing Control]
has_full_text: false
last_updated: 2026-06-23
---

## Abstract

Multi-fuel compression ignition (CI) engines offer high power density and fuel flexibility but face significant challenges in maintaining optimal combustion phasing across varying operating conditions and fuel types, particularly in the presence of modeling uncertainties. This paper presents a data-driven real-time uncertainty compensation framework for combustion control in multi-fuel CI engines. A Gaussian Process Regression (GPR) model is first trained to capture the nonlinear, fuel-dependent combustion behavior. A pseudo-engine-speed variable is introduced to enable dynamic adaptation of control inputs in response to real-time uncertainty, without requiring explicit fuel identification. The companion journal paper is published in the Proceedings of the Institution of Mechanical Engineers, Part I (DOI: 10.1177/09596518251399937).

## Key Contributions

- **Novel pseudo-engine-speed concept**: A virtual variable that encodes uncertainty information and enables real-time control adaptation without fuel type identification — significantly simplifies the control architecture.
- **GPR-based combustion model**: Captures nonlinear, fuel-dependent combustion behavior with natural uncertainty quantification, enabling principled uncertainty compensation.
- **Real-time uncertainty compensation**: Framework adapts combustion phasing control in real time to handle model-plant mismatch across fuel blends and operating conditions.
- **Validated on multi-fuel CI engine**: Practical demonstration on a challenging powertrain platform (U.S. Army Research Laboratory collaboration).
- **Published companion journal paper**: Demonstrates industrial-level maturity and peer validation.

## Methods

- **Gaussian Process Regression (GPR)**: Data-driven surrogate model trained on combustion input-output data; provides both mean prediction and uncertainty estimates used directly for control.
- **Pseudo-engine-speed variable**: A derived signal that compresses uncertainty information into a single scalar; used as a scheduling variable for control adaptation.
- **Combustion phasing control**: Target: maintain optimal CA50 (crank angle of 50% heat release) across fuel blends and load conditions.
- **Data-driven framework structure**: Offline GPR training → online uncertainty estimation → real-time control law adaptation.

## Key Results

- Achieves consistent combustion phasing across multi-fuel operating conditions (quantitative results in published companion paper DOI:10.1177/09596518251399937).
- Framework enables dynamic control adaptation without real-time fuel identification — practical advantage for military/multi-fuel applications.
- Validated experimentally on hardware.

## Limitations / Open Questions

- GPR scales poorly with training data size (O(n³) complexity) — may limit applicability to large operating-condition spaces or online re-training.
- Pseudo-engine-speed concept requires careful calibration; physical interpretability is limited.
- Framework designed for CI engines; applicability to SI engines or electric/hybrid powertrains requires adaptation.
- Uncertainty compensation loop bandwidth not characterized — stability under fast transients may be limited.
- Fuel sensor-free design is a strength, but also means real fuel composition is never explicitly known; edge cases with extreme blends may challenge the GPR extrapolation.

## Research Ideas

1. **GPR-based adaptive energy management for hybrid electric vehicles**: Apply the GPR uncertainty compensation framework to HEV energy management, where battery aging, temperature variation, and driver demand uncertainty create real-time modeling errors similar to multi-fuel combustion variability. The pseudo-scheduling-variable concept maps naturally to a "pseudo-battery-state" that absorbs uncertainty. Connects to [[data-driven-partitioning-energy-management]] and [[vedula-2026-predictive-energy-hybrid-powertrain]].

2. **Sparse GP or GP approximation for real-time vehicle control**: The cubic scaling of GPR limits its online use in fast vehicle control loops. Investigating sparse GP (inducing points) or GP approximations (random Fourier features) for real-time combustion/powertrain control would enable deployment at vehicle ECU frequencies (>100 Hz), making this framework practical for production vehicles. This is a methods-level contribution to [[AI-based-vehicle-control]].

## Connections

- [[noncentralized-mpc]] — The modular data-driven approach is compatible with distributed MPC architectures.
- [[data-driven-partitioning-energy-management]] — GPR-based uncertainty modeling directly applicable to EV energy management.
- [[vedula-2026-predictive-energy-hybrid-powertrain]] — Both address adaptive energy/powertrain control; different actuation domains (engine combustion vs. hybrid split).
- [[zhang-2026-koopman-mpc-time-delayed]] — Both address data-driven robust control; Koopman vs. GP modeling philosophies.
- Related concept (future): `gaussian-process-control`, `combustion-control`.

## Notable Quotes / Figures

> "A pseudo-engine speed...enables dynamic adaptation of control inputs in response to uncertainty affecting the engine." — from abstract
