---
title: "Personalized Electric Vehicle Energy Consumption Estimation Framework that Integrates Driver Behavior with Map Data"
type: paper
authors: [Rachavelpula, Sreechakra Vasudeva Raju, Cha, Sangwhan]
year: 2026
journal: arXiv preprint
doi: arxiv:2604.20764
tags: [electric-vehicle, energy-estimation, driver-behavior, personalization, BiLSTM, regenerative-braking, SOC, map-data, eco-driving]
methods: [BiLSTM, PID Controller, Physics-Based Energy Model, Route Processing, Quasi-Steady Model]
has_full_text: false
last_updated: 2026-06-23
---

## Abstract

This paper presents a personalized BEV energy consumption estimation framework that combines map-based road context with individual driver behavior modeling. The pipeline includes route selection, road feature extraction, a rule-based reference velocity generator, a PID-based vehicle dynamics simulator, and a Bidirectional LSTM trained to reproduce individual driver velocity profiles. The driver-specific velocity predictions are coupled with a quasi-steady backward energy consumption model to compute tractive power, regenerative braking energy, and SOC evolution. Evaluation across urban, freeway, and hilly routes shows accurate capture of driver-specific patterns (deceleration at intersections, speed-limit tracking, grade response) and accurate power/SOC trajectories.

## Key Contributions

- **End-to-end personalized pipeline**: From route map → road features → personalized velocity prediction → energy/SOC estimation, in a single coherent framework.
- **Driver behavior modeling via BiLSTM**: Learns individual-specific driving patterns (not population averages), enabling personalization beyond rule-based approaches.
- **Regenerative braking integration**: Explicitly models regenerative braking energy recovery in the backward energy computation.
- **Multi-terrain validation**: Urban, freeway, and hilly routes demonstrate robustness across diverse driving conditions.
- **Physics-based energy model**: Quasi-steady backward model ensures physical consistency of energy estimates.

## Methods

- **Route processing**: Map-based road feature extraction (grade, speed limits, intersection locations).
- **Reference velocity generator**: Rule-based generator using road context as prior for velocity shaping.
- **PID vehicle dynamics simulator**: Simulates realistic vehicle speed response to driver inputs.
- **BiLSTM**: Learns individual driver deviations from the reference velocity profile; trained per-driver on historical data.
- **Quasi-steady backward energy model**: Computes tractive force, rolling resistance, aerodynamic drag, grade force → power demand → battery power → SOC evolution, with regenerative braking captured on deceleration events.

## Key Results

- Captures driver-specific behaviors: deceleration patterns at intersections, speed-limit adherence, road-grade responses.
- Produces accurate power and SOC trajectories across urban, freeway, and hilly routes.
- Quantitative accuracy metrics (RMSE/MAE) not reported in retrieved abstract.
- Regenerative braking energy recovery is explicitly modeled and captured in SOC curves.

## Limitations / Open Questions

- BiLSTM requires per-driver historical training data; cold-start problem for new drivers is unaddressed.
- Quasi-steady energy model neglects transient drivetrain dynamics (inertia effects at high accelerations); may under-predict energy in aggressive driving.
- Weather/temperature effects on battery and tire rolling resistance are not modeled.
- Real-time range estimation capability not demonstrated (offline framework).
- Generalization across different BEV models (different powertrain efficiencies) requires retraining.

## Research Ideas

1. **Meta-learning for rapid driver personalization**: Apply MAML or prototypical networks to enable rapid adaptation of the BiLSTM driver model to new drivers with only a few trips of data. This addresses the cold-start problem and enables fleet-scale personalized range estimation — directly connecting to Prof. Kim's [[adaptive-personalized-vehicle-control]] research area.

2. **Closed-loop personalized eco-driving controller**: Invert the estimation pipeline into a control policy: use the personalized driver model to predict future energy consumption and feed it into an MPC that nudges the driver (via speed advisory or haptic feedback) toward more energy-efficient behavior while respecting their individual style. This creates a personalized ADAS with provable energy savings, building on [[noncentralized-mpc]] and [[eco-driving]].

3. **Physics-informed regenerative braking optimization within the personalization framework**: Replace the fixed quasi-steady regen model with an optimizable regen profile that adapts to driver deceleration patterns, maximizing energy recovery subject to brake comfort and stability constraints. Relevant to [[regenerative-braking]] and [[safety-dynamics-electrified-vehicles]].

## Connections

- [[vehicle-state-estimation]] — SOC estimation is a core output of this framework.
- [[labib-2026-battery-voltage-dmdc-transformer]] — Complementary: accurate battery voltage dynamics would improve the SOC computation.
- [[he-2026-eco-driving-ev-multi-speed]] — Both address eco-driving for EVs; this paper focuses on personalization, He et al. on multi-speed powertrain optimization.
- [[adaptive-partitioning-ev-chassis]] — Personalized control connects to the adaptive distributed MPC research idea.
- Related concept (future): `driver-behavior-modeling`, `range-estimation`.

## Notable Quotes / Figures

> "The framework couples predicted individual-specific velocity profiles with a quasi-steady backward energy consumption model to compute tractive power, regenerative braking, and State-of-Charge (SOC) evolution." — from abstract
