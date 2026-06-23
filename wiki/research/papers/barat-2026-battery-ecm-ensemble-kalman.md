---
title: "System Identification of Lithium-Ion Battery Equivalent Circuit Models Using Ensemble Kalman Inversion"
type: paper
authors: [Barat, Farzaneh, Wilson, Sara, Kim, Huijeong, Fang, Huazhen]
year: 2026
journal: arXiv preprint
doi: arxiv:2604.10813
tags: [battery, system-identification, ECM, ensemble-Kalman, parameter-estimation, lithium-ion, BMS]
methods: [Ensemble Kalman Inversion, ECM, Maximum A Posteriori Estimation, Gaussian Approximation]
has_full_text: false
last_updated: 2026-06-23
---

Submitted April 12, 2026 (University of Kansas + Michigan State University). Applies Ensemble Kalman Inversion (EnKI) — a derivative-free, ensemble-based optimization method — to identify parameters of lithium-ion battery equivalent circuit models (ECMs). EnKI performs maximum a posteriori parameter estimation through successive local Gaussian approximations, avoiding gradient computation on the nonlinear battery model. Complements [[labib-2026-battery-voltage-dmdc-transformer]] (dynamics modeling) by providing robust ECM parameter identification — the ECM parameters feed directly into UKF/EKF-based SOC estimators central to [[vehicle-state-estimation]]. Relevant to area 5 (Vehicle state and parameter estimation) and area 4 (Optimal control for electrified powertrains).
