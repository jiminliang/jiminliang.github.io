---
title: AI for Computational Electromagnetics (AI4CEM)
date: 2026-03-13
image:
  focal_point: 'top'
---

We are developing AI models for computational electromagnetics.

<!--more-->

<font size=3>

## Introduction

Accurate electromagnetic scattering analysis is a core problem in computational electromagnetics. It supports a wide range of engineering applications, including radar cross section (RCS) evaluation, stealth analysis, and electromagnetic structure design. In practice, however, these tasks rarely require just one simulation. Engineers often need to evaluate many candidate structures, repeatedly adjust geometry, test different incident-wave conditions, and iterate through a long design loop before reaching a satisfactory solution.

This is where the bottleneck appears. Traditional full-wave numerical solvers are highly reliable and physically rigorous, but they are also computationally expensive. For complex 3D objects, each simulation can take tens of seconds or much longer, and repeated evaluations quickly become costly. From the perspective of engineering workflow, the issue is not that full-wave solvers are inadequate, but that they are too expensive to invoke again and again during early-stage exploration and rapid iteration.

This observation motivated our work. Instead of trying to replace classical computational electromagnetics, **we asked whether a data-driven surrogate model could be used to accelerate the repeated evaluation stage of the design process**.

## Why This Problem Is Challenging

Learning-based electromagnetic models have attracted increasing attention in recent years, but most existing approaches remain limited in one or more important ways. Many works focus on two-dimensional settings, simplified geometries, single-frequency prediction, or low-dimensional intermediate representations. For realistic 3D scattering problems, the difficulty is much higher.

One central challenge is the representation of geometry itself. Electromagnetic scattering is highly sensitive to detailed surface shape, global topology, and incident-wave configuration. If the geometric representation is too coarse, too indirect, or too detached from the physics, the learned model easily loses the information needed for accurate prediction.

This is why our work starts from a different point. Rather than converting the object into voxels, hand-designed descriptors, or other heavily processed forms, **we directly use the 3D triangular surface mesh as input and learn a mapping from surface geometry and incident-wave parameters to the scattering response**. In this sense, the model operates much closer to the actual computational representation used by numerical electromagnetics.

## Our Method: GTC-3DEM

The proposed framework is called **GTC-3DEM**, short for Graph-Transformer-Convolutional 3D Electromagnetic surrogate model.

Its core idea is to combine geometric representation learning with physically meaningful conditioning:

- The 3D object is represented as a triangular surface mesh.
- Each triangular facet is treated as a graph node with geometric and electromagnetic attributes.
- A graph neural network captures local interactions among neighboring mesh facets.
- A Transformer module models longer-range dependencies across the whole object.
- A convolutional decoder reconstructs the final 2D RCS pattern.
- A hierarchical conditioning mechanism injects global incident-wave parameters, such as direction and frequency, throughout the network.

This design reflects an important physical intuition. Local surface interactions matter, but wideband scattering is also influenced by more global geometric structure and long-range coupling effects. By combining graph-based local modeling, Transformer-based global aggregation, and structured decoding, GTC-3DEM learns an end-to-end surrogate mapping from **3D surface geometry directly to scattering output**.

This point is important. Many existing learning-based methods do not directly learn from the target’s 3D surface representation to its final RCS response in such a direct and scalable way. In our view, this direct geometry-to-scattering mapping is one of the main strengths of the work.

## What We Found

The results show that GTC-3DEM can serve as an effective surrogate model for wideband 3D electromagnetic scattering computation.

Most notably, once trained, the model reduces per-sample RCS prediction time from **tens of seconds to less than 0.2 seconds**, while maintaining strong accuracy on in-distribution test cases. This makes the framework especially attractive in settings where a large number of repeated evaluations are needed.

The study also shows that the framework is reasonably robust across multiple practical factors, including:

- wideband frequency variation
- mesh resolution changes
- different incident-wave configurations
- polarization extension
- prediction of other electromagnetic quantities such as electric fields

These experiments indicate that the framework is not just solving one narrow benchmark task, but has the potential to become a more general surrogate modeling tool for computational electromagnetics.

At the same time, the paper also makes the limitations clear. Out-of-distribution performance degrades when the test geometries differ substantially from the dominant patterns in the training set. The current model is also restricted to PEC objects and remains fundamentally dependent on high-fidelity simulation data for training. In other words, **the model is fast because it learns from expensive numerical simulations, not because it eliminates the need for them altogether**.

## Why This Matters for Engineering

This is the point we consider most important from an application perspective.

Our goal is **not** to claim that a data-driven surrogate can replace traditional numerical electromagnetic solvers in all scenarios. It cannot. In terms of ultimate physical reliability, accuracy guarantees, and generalization to truly arbitrary geometries and materials, classical full-wave methods remain indispensable.

However, engineering design is rarely a one-shot computation problem. It is usually an iterative process:

1. propose a design
2. evaluate its scattering response
3. modify the geometry
4. evaluate again
5. repeat many times

When this loop is driven entirely by conventional simulation, the turnaround cost can become a major obstacle. A surrogate model such as GTC-3DEM offers value precisely here. It can act as a **fast approximation engine** for rapid screening, early-stage exploration, sensitivity analysis, or iterative optimization, allowing engineers to traverse the design space much more efficiently before resorting to expensive high-fidelity verification.

In that sense, the model should be understood as a complement to numerical electromagnetics, not a substitute. Full-wave solvers remain the final authority. The surrogate model is the accelerator that makes the overall design workflow more practical.

## A First Step Toward AI4CEM

We view this work as an early step in a broader research direction: **AI for Computational Electromagnetics (AI4CEM)**.

The broader vision is to develop learning-based models that can work together with classical electromagnetic computation, combining the speed of neural surrogates with the rigor of physics-based simulation. GTC-3DEM demonstrates that this idea is already viable in an important 3D scattering setting. It shows that deep learning can be used not merely for post-processing or inverse tasks, but as a practical surrogate component in the electromagnetic analysis pipeline.

Of course, many challenges remain. Better geometric diversity, support for non-PEC materials, stronger out-of-distribution generalization, and more physics-guided learning strategies are all important next steps. But as a proof of concept, this work shows a clear engineering opportunity: **AI can help computational electromagnetics not by replacing physics, but by accelerating the many repetitive computations that slow engineering iteration down**.

Read our paper for more details:

Xiaotian Jiang, Huan Huan Zhang, Kaitai Guo, Yang Zheng, Jimin Liang, [Mesh-Based Deep Learning Surrogate Model for Rapid Wideband 3D Electromagnetic Scattering Computation](https://ieeexplore.ieee.org/document/11412392), *IEEE Transactions on Antennas and Propagation*, 2026.

</font>
