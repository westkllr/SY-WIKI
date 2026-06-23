---
title: "Operator-Theoretic and Physics-Guided Sequence Modeling of Lithium-Ion Battery Voltage Dynamics"
type: paper
authors: [Labib, Khalid Mahmud, Rasool, Inayat, Ahmed, Shabbir]
year: 2026
journal: arXiv preprint
doi: arxiv:2605.01693
tags: [battery-modeling, DMDc, physics-guided, transformer, lithium-ion, state-estimation, electrified-powertrain, HPPC, operator-theory]
methods: [DMDc, Dynamic Mode Decomposition with Control, Physics-Guided Transformer, PatchTST, HPPC, Delay Embedding]
has_full_text: false
last_updated: 2026-06-23
---

## Abstract

Lithium-ion batteries exhibit strongly nonlinear voltage dynamics that vary with operating conditions and cell aging, making accurate data-driven modeling essential for estimation, control, and health monitoring. This paper compares two frameworks for modeling voltage responses from hybrid pulse power characterization (HPPC) data: an operator-theoretic model using Dynamic Mode Decomposition with control (DMDc) with delay-embedded snapshots, and a physics-guided transformer (modified PatchTST) that decomposes terminal voltage into an analytically computed OCV component and a learned dynamic residual. On a 30 Ah lithium-ion cell, DMDc achieves lower prediction error and greater robustness to cell degradation under limited data, while the transformer captures similar dynamics with greater architectural flexibility.

## Key Contributions

- **Side-by-side comparison** of operator-theoretic (DMDc) vs. deep-learning (physics-guided transformer) approaches on identical HPPC data.
- **Physics-guided PatchTST**: Terminal voltage decomposed into OCV (analytical) + dynamic residual (learned), with a future-current fusion pathway tailored to HPPC current profiles.
- **Delay-embedded DMDc**: Uses time-delayed voltage/current snapshots to identify linear state-space dynamics, enabling interpretable recursive prediction.
- **Aging robustness finding**: DMDc outperforms under cell degradation when data is limited — important practical result for BMS deployment.
- **Transparent model comparison** on shared 30 Ah cell dataset.

## Methods

- **DMDc (Dynamic Mode Decomposition with Control)**: Delay-embedded snapshots of terminal voltage and current → linear system matrices directly from data → recursive state-space prediction.
- **Modified PatchTST (Physics-Guided Transformer)**: OCV computed analytically from SOC; transformer learns the dynamic overpotential residual; future current injected as conditioning signal.
- **HPPC (Hybrid Pulse Power Characterization)**: Standard battery test profile with charge/discharge pulses; used to capture transient dynamics across SOC levels.
- **Dataset**: 30 Ah lithium-ion cell; multiple aging levels tested.

## Key Results

- DMDc achieves **lower prediction error** and **greater robustness under cell degradation** in the limited-data regime.
- Physics-guided transformer captures qualitatively similar dynamics with greater flexibility — better suited when abundant data exists.
- Both models capture sharp transient pulse dynamics characteristic of HPPC profiles.
- Quantitative RMSE values not reported in search-retrieved abstract.

## Limitations / Open Questions

- Results on a single 30 Ah cell; generalizability to other chemistries (LFP, NMC) and form factors (cylindrical, pouch) is open.
- HPPC-only training may not capture dynamics under realistic driving current profiles (WLTP, UDDS).
- Transformer requires more data — not yet validated under data-scarce conditions for online BMS deployment.
- DMDc assumes quasi-linear dynamics after delay embedding; strongly nonlinear aging effects may break this assumption at high degradation levels.
- Neither model appears to incorporate temperature effects, which significantly affect Li-ion dynamics.

## Research Ideas

1. **Online adaptive DMDc for real-time BMS**: Extend DMDc to an online, recursive update scheme (similar to online DMD or extended DMD) that tracks slowly varying battery parameters as the cell ages, enabling real-time SOC and SOH estimation without re-identification. This is directly feasible using existing tools for online DMD and relevant to [[vehicle-state-estimation]].

2. **Physics-guided PINN battery model for EV co-simulation**: Embed the physics-guided transformer structure (OCV + residual) into a [[physics-informed-neural-networks]] framework with electrochemical constraints (e.g., Butler-Volmer, diffusion PDE) to enable co-simulation with vehicle dynamics and powertrain control — bridging battery modeling and [[optimal-control-electrified-powertrain]].

## Connections

- [[vehicle-state-estimation]] — Battery voltage/SOC estimation is a key component of EV state estimation.
- [[schafke-2026-virtual-wheel-speed-sensor]] — Complementary work: estimation on the mechanical vs. electrochemical side of EVs.
- [[rachavelpula-2026-personalized-ev-energy]] — That paper's SOC modeling relies on accurate battery dynamics; this work improves the modeling foundation.
- Related concept (future page): `battery-modeling` — covers ECM, physics-based, data-driven approaches.
- [[barat-2026-battery-ecm-ensemble-kalman]] — Complementary: parameter identification vs. dynamics modeling.

## Notable Quotes / Figures

> "Although both models capture the sharp transient pulse dynamics, DMDc achieves lower prediction error and greater robustness to cell degradation under the present limited data regime, while the transformer captures qualitatively similar dynamics with greater architectural flexibility." — from abstract
