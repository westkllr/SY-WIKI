---
title: "Neural Network-Based Virtual Wheel-Speed Sensor for Enhanced Low-Velocity State Estimation"
type: paper
authors: [Schäfke, Hendrik, Weber, Daniel O. M., Vagapov, Askar, Schweers, Christoph, Seel, Thomas, Ehlers, Simon F. G.]
year: 2026
journal: arXiv preprint (accepted to IFAC World Congress 2026, Busan, Korea)
doi: arxiv:2605.12230
tags: [vehicle-state-estimation, virtual-sensor, neural-network, wheel-speed, UKF, electric-vehicle, ADAS, low-velocity]
methods: [Neural Network, UKF, Sensor Fusion, Virtual Sensor]
has_full_text: false
last_updated: 2026-06-23
---

## Abstract

Conventional wheel-speed sensors in electric vehicles suffer from quantization errors and latency at low velocities, while motor-speed signals are distorted by drivetrain torsion, degrading state estimation accuracy precisely when ADAS functions need it most. This paper presents a neural-network-based virtual wheel-speed sensor that fuses wheel-speed and motor-speed signals to suppress errors from both sources, validated on real-world Volkswagen ID.7 data. The proposed model achieves up to 85% error reduction compared to the production sensor and 47% compared to an optimized zero-phase filter, while remaining real-time capable.

## Key Contributions

- **Virtual sensor design**: Neural network that fuses wheel-speed and motor-speed signals to compensate for quantization errors and drivetrain torsion simultaneously.
- **Low-velocity focus**: Explicitly addresses the regime where conventional sensors fail most severely, which is critical for ADAS and low-speed parking/maneuver scenarios.
- **Real-world validation on Volkswagen ID.7**: Demonstrates strong generalization from simulation to production EV hardware.
- **Real-time capable implementation**: Suitable for embedded deployment in vehicle ECUs.
- **85% error reduction** over production sensor; 47% over optimized zero-phase filter.

## Methods

- **Sensor fusion architecture**: Combines wheel-speed encoder pulses and motor resolver/encoder signals as dual inputs.
- **Neural network (type unspecified in abstract)**: Learns the mapping from noisy sensor inputs to corrected wheel-speed estimates.
- **Unscented Kalman Filter (UKF)**: Used as the downstream state estimator; the virtual sensor output serves as a cleaner input.
- **Comparison baselines**: Production sensor, zero-phase digital filter.
- **Validation dataset**: Real-world drive data from Volkswagen ID.7 (production electric vehicle).

## Key Results

- Error reduction of **up to 85%** vs. production wheel-speed sensor.
- Error reduction of **up to 47%** vs. optimized zero-phase filter baseline.
- Real-time capable (no quantified latency reported in abstract, but stated as real-time suitable).
- Accepted to IFAC World Congress 2026 (Busan, Republic of Korea, August 2026) — peer-reviewed.

## Limitations / Open Questions

- Neural network architecture details not disclosed in the abstract; generalizability across different EV platforms unknown.
- Validation limited to Volkswagen ID.7; applicability to other drivetrains (AWD, in-wheel motors) unverified.
- Low-velocity threshold definition is unclear — performance at intermediate speeds not characterized.
- Robustness under sensor degradation (faulty encoder) not addressed.
- The UKF downstream estimator still relies on a physical vehicle model; model mismatch under varying payloads or road conditions is an open issue.

## Research Ideas

1. **Cross-platform virtual sensor transfer**: Apply domain adaptation or transfer learning to generalize the virtual wheel-speed sensor from the ID.7 to other EV platforms (AWD, in-wheel motor configurations) with minimal re-calibration data. Feasible given the availability of multiple production EV testbeds.

2. **Integrated PINN-based UKF with virtual sensor**: Replace the conventional UKF with a physics-informed neural network (PINN) state estimator that jointly learns the drivetrain torsion model and the wheel-speed correction, eliminating the modular boundary between virtual sensor and estimator. This directly bridges work on [[physics-informed-neural-networks]] and [[vehicle-state-estimation]].

3. **Extension to lateral velocity and slip angle estimation**: Use the improved wheel-speed signals as higher-quality inputs to a slip angle estimator (e.g., EKF/UKF with tire model), targeting the safety-critical lateral dynamics regime where sideslip and tire saturation occur at low speeds (e.g., parking lot maneuvers on slippery surfaces).

## Connections

- [[vehicle-state-estimation]] — Core contribution; improves the measurement input quality for state estimators.
- [[noncentralized-mpc]] — Cleaner state estimates could improve distributed MPC for chassis control.
- Related concept: [[adaptive-vehicle-control]] — Virtual sensor enables reliable low-speed control.
- Related paper (same venue): [[labib-2026-battery-voltage-dmdc-transformer]] — complementary estimation work for powertrain side.
- [[habich-2026-pinn-mpc-soft-robot]] — **동일 연구그룹** (Simon Ehlers 공저자, Leibniz Hannover iMeS). DD-PINN 기반 NMPC 논문; Research Idea #2의 PINN-UKF 통합 아이디어와 직접 연결.
- [[leibniz-imes-group]] — 공저자 소속 연구그룹 페이지; Ehlers의 차량 동역학 PINN 연구(Zeipel et al. 2024) 포함.
- [[pinn-surrogate-ev-nmpc]] — 이 논문 Research Idea #2를 확장한 EV NMPC 연구 아이디어.

## Notable Quotes / Figures

> "The real-time capable model achieves an error reduction of up to 85% compared to the production sensor and 47% compared to an optimized zero-phase filter." — from abstract
