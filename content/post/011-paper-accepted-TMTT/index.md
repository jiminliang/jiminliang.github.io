---
title: Paper accepted by IEEE Transactions on Microwave Theory and Techniques
date: 2026-11-01
image:
  focal_point: 'top'
---

Our paper on a condition-aware neural operator for 3D dielectric microwave scattering has been accepted by **[IEEE Transactions on Microwave Theory and Techniques](https://doi.org/10.1109/TMTT.2026.3750196)** - November 1, 2026.

<!--more-->

Microwave analysis and design often require repeated three-dimensional full-wave evaluation as geometry, dielectric material distribution, frequency, illumination, and observation direction change. This is particularly challenging for penetrable inhomogeneous objects, where scattering depends not only on the external shape but also on the internal volumetric permittivity and material interfaces. Repeated high-fidelity simulation across this large condition space can therefore become a major bottleneck in design exploration.

In this work, we introduce **GT-DieleNO**, a Graph-Tetrahedral Dielectric Neural Operator that represents each target as a tetrahedral volume graph with cell-wise material information. A volume-weighted graph neural-operator encoder, a Transolver-style latent mixer, and a DeepONet-style query decoder jointly map geometry, dielectric distribution, and microwave conditions to far-field response queries. The resulting model acts as a fast, reusable surrogate for material-, frequency-, incidence-, and observation-conditioned microwave evaluations rather than as a replacement for full-wave simulation.

The study constructs a multi-object dielectric benchmark with 84,600 dense simulated microwave response tensors and evaluates interpolation, held-material prediction, unseen-geometry generalization, architecture ablations, sparse measured-data fitting, and runtime. For one dense 360 x 720 RCS map, GT-DieleNO achieves a conservative **146.2x** online speedup over the tested FEM solve. These results demonstrate how AI can complement computational microwave techniques by accelerating repeated analysis and candidate screening while retaining full-wave solvers for high-fidelity verification.

The paper is accepted for publication with DOI [10.1109/TMTT.2026.3750196](https://doi.org/10.1109/TMTT.2026.3750196). Code and implementation details are available at [GT-DieleNO](https://github.com/cytosineXT/GT-DieleNO).

{{% cta cta_link="/highlights-ai4cem/003-GTDieleNO" cta_text="Read more ..." %}}
