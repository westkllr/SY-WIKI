---
title: "ARC: Adaptive Robust Joint State and Covariance Estimation"
type: paper
authors: [Hadji-Thomas, Alexandre, Stirling, Andrew, Forbes, James R.]
year: 2026
journal: arXiv preprint (submitted to IEEE Robotics and Automation Letters)
doi: arxiv:2606.20428
tags: [state-estimation, robust-estimation, covariance-estimation, outlier-rejection, non-Gaussian-noise, adaptive-estimation, sensor-fusion]
methods: [Robust Estimation, Covariance Estimation, Outlier Rejection, Joint State-Covariance Estimation, Non-Gaussian Noise Modeling]
has_full_text: false
last_updated: 2026-06-23
---

## Abstract

Classical state estimators produce biased and unreliable estimates when sensor measurements are corrupted by outliers or non-Gaussian noise. Prior work addresses either outlier rejection (robust estimators) or measurement covariance estimation (joint state-covariance estimators) but not both simultaneously — robust estimators assume known noise shape, while joint estimators assume Gaussian residuals. ARC (Adaptive Robust Combined) integrates both capabilities into a unified framework that simultaneously estimates state and covariance in the presence of outliers, resolving a long-standing gap in robust state estimation.

## Key Contributions

- **Unified robust + joint estimation**: First framework to simultaneously reject outliers and estimate measurement covariance — eliminates the need to assume either Gaussian noise or fixed loss shape parameters.
- **Adaptive robust estimation**: Loss shape parameters are adapted online alongside the state, enabling principled handling of time-varying, non-Gaussian noise distributions.
- **Broad applicability**: Designed for any sensor-based state estimation pipeline where measurements may be corrupted (LIDAR, camera, IMU, wheel encoders).
- **Submitted to IEEE RA-L**: High-quality robotics/automation venue signals rigorous peer review.

## Methods

- **Robust M-estimator framework**: Uses robust loss functions (e.g., Huber, Cauchy, or similar) to downweight outlier measurements.
- **Joint state and covariance estimation**: Alternating or simultaneous optimization of state and noise covariance parameters.
- **Adaptive loss shape**: Online adaptation of the robust loss function parameters based on residual statistics.
- **Implementation**: Presumably an iterative/optimization-based estimator (exact algorithm details not retrieved in abstract).

## Key Results

- Demonstrated simultaneous improvement in state estimation accuracy and covariance reliability under outlier-corrupted measurements.
- Specific benchmark results (quantitative error metrics) not retrieved from abstract.
- Submitted to IEEE Robotics and Automation Letters — targeted for high-impact application in robotics and autonomous systems.

## Limitations / Open Questions

- Full algorithm details and computational complexity not available from abstract alone.
- Real-time performance on embedded hardware (vehicle ECU or robot onboard computer) not characterized.
- Convergence guarantees under rapid outlier rate changes are unclear.
- Application to vehicle-specific sensors (wheel encoders, IMU, GPS dropout scenarios) not explicitly demonstrated.
- Robustness to adversarial or structured noise (e.g., GPS spoofing, sensor drift) not addressed.

## Research Ideas

1. **ARC for vehicle state estimation under harsh road conditions**: Apply the ARC framework to multi-sensor vehicle state estimation (IMU + wheel encoders + GPS + camera) where road roughness, tunnels, and wet road conditions introduce intermittent outliers and non-Gaussian noise. The framework's ability to adapt covariance online is critical for real-time chassis control. Directly relevant to [[vehicle-state-estimation]].

2. **Robust joint estimation for battery state in EVs**: Adapt ARC-style joint robust estimation to EV battery management, where current and voltage sensors can suffer from quantization errors, temperature-induced drift, and occasional spikes. Online covariance adaptation would improve SOC/SOH estimation reliability across aging cells. Links to [[labib-2026-battery-voltage-dmdc-transformer]] and [[barat-2026-battery-ecm-ensemble-kalman]].

## Connections

- [[vehicle-state-estimation]] — Direct application domain for robust state estimation.
- [[schafke-2026-virtual-wheel-speed-sensor]] — Complementary: virtual sensor corrects measurement quality upstream; ARC handles residual outliers in the estimator itself.
- [[labib-2026-battery-voltage-dmdc-transformer]] — Robust covariance estimation would improve battery state estimation reliability.
- Related concept (future): `robust-estimation`, `covariance-estimation`.

## Notable Quotes / Figures

> "Robust estimators reject or downweight outliers but do not perform measurement covariance estimation, whereas joint state and covariance estimators assume Gaussian residuals and fixed loss shape parameters. Integrating these two capabilities into a single framework is an opportunity to simultaneously estimate both state and covariance in the presence of outliers." — from abstract
