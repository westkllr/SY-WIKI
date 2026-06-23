---
title: "Frequency-Domain Neural ODEs for Modeling Non-Linear Dynamical Systems"
type: paper
authors: [Ashraf, Mohammed, El-Badawy, Ayman A.]
year: 2026
journal: arXiv preprint
doi: arxiv:2606.22075
tags: [neural-ODE, frequency-domain, FFT, nonlinear-dynamics, system-identification, data-driven-modeling]
methods: [Neural ODE, FNODE, Fast Fourier Transform, Frequency Domain Learning]
has_full_text: false
last_updated: 2026-06-23
---

Submitted June 20, 2026 (German University in Cairo, Egypt). Proposes FNODE (Frequency-domain Neural ODE), which projects continuous temporal dynamics into the frequency domain via Fast Fourier Transform before integration. Standard Neural ODEs struggle with highly nonlinear dynamics; operating in the frequency domain improves generalization by separating dominant oscillatory modes from noise. Relevant to vehicle dynamics system identification — nonlinear lateral and longitudinal vehicle dynamics exhibit frequency-separated modes (slow body, fast tire) that FNODE could capture more efficiently than time-domain Neural ODEs. Potential application to [[vehicle-state-estimation]] and [[AI-based-vehicle-control]].
