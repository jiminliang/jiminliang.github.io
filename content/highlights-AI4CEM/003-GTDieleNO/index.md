---
title: Condition-Aware Neural Operator for 3D Dielectric Microwave Scattering
date: 2026-11-01
image:
  focal_point: 'top'
---

We are developing condition-aware AI models for microwave full-wave surrogate modeling.

<!--more-->

<font size=3>

## Introduction

Accurate microwave analysis of three-dimensional dielectric objects is essential in electromagnetic design, material characterization, sensing, and scattering studies. In a realistic design loop, however, engineers rarely evaluate one fixed object under one fixed condition. They vary the geometry, redistribute the dielectric material inside the target, sweep frequency, change illumination, and inspect the response over many observation directions. Each variation can require another full-wave solution, so repeated high-fidelity simulation quickly becomes the dominant cost.

Our earlier work, GTC-3DEM, showed that a deep surrogate model can accelerate 3D electromagnetic scattering prediction directly from geometry. That study focused mainly on perfect-electric-conductor targets, where the outer surface carries the essential electromagnetic behavior. Many microwave problems are different: the target is penetrable, and its interior material distribution is part of the physics. Two objects with the same outer shape can produce very different responses when their permittivity distributions differ.

This motivated our new work: **can a single learned operator represent a dielectric volume together with its microwave conditions and answer many far-field response queries without solving the full-wave problem again for every query?**

## Why Dielectric Scattering Is Harder

For a penetrable target, scattering depends not only on the outer boundary but also on the volumetric permittivity field, internal material interfaces, field penetration, and multiple scattering inside the object. Frequency, incidence direction, and observation direction are also strongly coupled to that material structure. A useful surrogate therefore needs a representation that carries geometry and material information together, rather than treating dielectric properties as a simple class label.

Surface meshes are natural for exterior shapes and perfectly conducting objects. For inhomogeneous dielectrics, however, an exterior-only representation does not fully describe the material distribution. Regular voxel grids provide volume information but can introduce axis-aligned boundaries and limited resolution at oblique interfaces. Point clouds are flexible but require an additional rule for defining closed volume support and connectivity.

We chose a tetrahedral volume graph for this problem. It provides boundary-conforming volume cells, shared-face adjacency, cell-wise permittivity, and physical cell-volume weights in one unstructured representation. This choice is tailored to the dielectric scattering task rather than a claim that one geometric representation is universally best.

## Our Method: GT-DieleNO

The proposed framework is called **GT-DieleNO**, short for Graph-Tetrahedral Dielectric Neural Operator.

Each target is represented as a graph whose nodes correspond to tetrahedral cells. Every node carries geometric and material information, including its position, cell volume, and relative permittivity. Electromagnetic conditions are injected into the representation through the incident wave and frequency. The network then processes this conditioned volume through three complementary components:

- A volume-weighted graph neural-operator encoder captures local interactions while accounting for the physical size of each tetrahedral cell.
- A Transolver-style latent mixer aggregates information over the entire target and models longer-range coupling.
- A DeepONet-style query decoder maps the learned latent representation and an observation direction to the corresponding far-field response.

This architecture reflects an important shift in perspective. The learned object is not merely an image predictor that returns one fixed output grid. It is a **queryable operator** that combines a dielectric target and its illumination conditions with observation coordinates. Radar cross section (RCS) maps are used as the dense full-wave observable in the simulated benchmarks, but the broader interface is intended for fast, repeated evaluation of microwave responses across geometry, material, frequency, incidence, and observation variables.

We also built a multi-object microwave benchmark to evaluate the method beyond a single proof-of-concept target. The main dataset contains 20 aircraft-like objects, 10 dielectric material designs, three incidence settings, and 91 frequencies, producing 54,600 dense full-wave tensors. A 100-object geometry-scaling extension contributes another 30,000 tensors. Together, the study contains 84,600 dense simulated microwave responses.

## What We Found

The results show that GT-DieleNO can serve as an effective surrogate for dielectric microwave scattering in the studied setting.

Under frequency and condition interpolation on known geometries, the model reaches an independent-test PSNR of **29.05 dB**, SSIM of **0.9291**, and MSE of **0.0356**. Across five test geometries, PSNR remains between 27.68 and 30.41 dB, showing that the strong interpolation result is not driven by one favorable object.

The held-material experiments test whether the model can use the per-tetrahedron permittivity field rather than memorize a material identifier. Representative homogeneous and part-wise inhomogeneous targets retain their principal angular structures when a material design is withheld. At the same time, accuracy varies substantially with the held layout, especially when a test material lies near the edge of the represented range. This spread is an important part of the result: it identifies material-conditioned performance and its worst-case limitations rather than reporting only favorable averages.

The most demanding test uses unseen geometries within the same aircraft-like object family. GT-DieleNO reaches **12.75 dB** PSNR on the 20-object external test and **14.17 dB** on the same external test after geometry coverage is expanded to 80 training objects. The improvement is consistent across all matched folds, showing that broader geometric coverage helps. The lower absolute accuracy than the interpolation setting also makes the remaining challenge clear: unseen geometry is still the dominant difficulty.

The computational benefit is substantial. For one dense **360 x 720** single-frequency RCS map, GT-DieleNO requires about **0.1026 seconds**, compared with **15.00 seconds** for the tested finite-element full-wave solve at 0.55 GHz. This corresponds to a conservative **146.2x** online speedup for repeated dense-map evaluation.

We further test the query interface on sparse measurements from the Institut Fresnel dielectric scattering database. The model follows the dominant receiver-angle lobes in the held-condition examples. This experiment evaluates same-target fitting and should not be read as proof of transfer from simulation to unseen measured objects; it shows that the operator interface can accommodate sparse measured response queries with appropriate preprocessing.

These results support a focused conclusion. GT-DieleNO is not a replacement for a full-wave solver. It is a fast, reusable model for repeated evaluations within the material, frequency, illumination, and geometry domains represented by its training data.

## Why This Matters for Microwave Engineering

Microwave design and analysis often involve many related evaluations rather than one isolated simulation. A designer may need to compare several material layouts, sweep frequency, inspect multiple incidence conditions, or scan a dense set of observation directions. Full-wave solvers remain indispensable for physical fidelity, but invoking them at every point in that inner loop can dominate the total turnaround time.

GT-DieleNO targets exactly this bottleneck. Its value is to provide a **fast screening and analysis module** that can traverse a large condition space before expensive high-fidelity verification is reserved for the most promising cases. The same operator interface can accept different tetrahedral targets and material fields and return either dense angular maps or selected far-field queries.

The work also shows why the representation of material matters. A dielectric surrogate should not only learn what an object looks like from the outside; it should learn how the volumetric electromagnetic property participates in the response. By combining tetrahedral geometry, cell-wise permittivity, volume-aware aggregation, and query-based decoding, GT-DieleNO moves the surrogate closer to the structure of the underlying microwave problem.

## A Further Step Toward AI4CEM

We view GT-DieleNO as a further step in our **AI for Computational Electromagnetics (AI4CEM)** direction.

GTC-3DEM established a direct path from 3D surface geometry to scattering responses. GT-DieleNO extends that path from surface-dominated conducting targets to penetrable, inhomogeneous dielectric volumes. It treats material distribution as a physical input, conditions the learned response on microwave operating variables, and decouples the target representation from individual far-field query locations.

Many challenges remain. Generalization to more diverse geometries is still difficult; the current simulated study uses a fixed polarization and real-valued relative permittivity; complex material responses, mixed dielectric-conductor targets, and broader measured-data transfer require further work. Training also depends on high-quality full-wave data, so the surrogate accelerates repeated evaluation rather than eliminating the need for physics-based simulation.

Even with these boundaries, the engineering direction is clear: **AI can make computational electromagnetics more useful in practice by learning reusable operators that preserve the material and geometric structure of the problem while accelerating the many repeated evaluations required for microwave analysis and design**.

Read our paper for more details:

Xiaotian Jiang, Junming Hou, Kaitai Guo, Yang Zheng, Jian Wei You, Jimin Liang, *A Condition-Aware Dielectric Neural Operator for Microwave Full-Wave Surrogate Modeling of 3-D Inhomogeneous Scattering*, **IEEE Transactions on Microwave Theory and Techniques**, accepted for publication Nov. 1, 2026. [DOI: 10.1109/TMTT.2026.3750196](https://doi.org/10.1109/TMTT.2026.3750196). [Code and implementation details](https://github.com/cytosineXT/GT-DieleNO)

</font>
