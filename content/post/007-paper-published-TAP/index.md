---
title: Paper published by IEEE Transactions on Antennas and Propagation 
date: 2026-02-28
image:
  focal_point: 'top'
---

Our paper on [3D Surrogate Model for Electromagnetic Scattering Computation](https://ieeexplore.ieee.org/document/11412392) has been published by **IEEE Transactions on Antennas and Propagation** - February 28, 2026. 

<!--more-->

Accurate electromagnetic scattering analysis is a core problem in computational electromagnetics, underpinning applications such as radar cross-section evaluation, electromagnetic design, and stealth technology. In practical engineering workflows, however, electromagnetic solvers are often repeatedly invoked to evaluate many candidate structures under different incident-wave conditions. While full-wave numerical methods provide high fidelity, their computational cost makes large-scale design exploration and rapid iterative optimization extremely time-consuming.

In this work, we explore a learning-based approach to accelerate this evaluation process. The proposed framework, GTC-3DEM, leverages deep neural networks operating directly on triangular surface meshes to learn the mapping between object geometry, incident-wave parameters, and the resulting scattering response. Rather than replacing traditional numerical solvers, the goal is to provide a fast surrogate model that can rapidly estimate scattering behavior once trained on high-fidelity simulation data. After a one-time training stage, the model can produce wideband RCS predictions in less than 0.2 seconds per query, enabling efficient evaluation when a large number of scattering computations are required.

This study represents the first step of our laboratory toward the emerging research direction of AI for Computational Electromagnetics (AI4CEM). Our long-term goal is to develop learning-based electromagnetic models that complement classical numerical solvers, enabling faster design exploration and scalable electromagnetic analysis. Building upon this initial work, we are continuing to investigate physics-informed architectures, broader material modeling, and more general geometric representations for AI-driven electromagnetic computation.