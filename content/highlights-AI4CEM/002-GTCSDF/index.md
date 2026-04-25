---
title: SDF for 3D EMS Geometry Generalization
date: 2026-04-25
image:
  focal_point: 'top'
---

We are developing SDF-based AI models for computational electromagnetics.

<!--more-->

<font size=3>

## Introduction

Accurate three-dimensional electromagnetic scattering computation remains a central problem in computational electromagnetics. It underlies radar cross section (RCS) analysis, stealth-oriented aircraft assessment, and many other engineering workflows that require repeated wideband evaluations of complex targets. In practice, the challenge is not merely to solve one scattering problem well, but to solve many of them efficiently across changing geometries, frequencies, and incident directions.

This is exactly where conventional full-wave solvers become expensive. They remain the gold standard in physical fidelity, but repeated simulation over complex 3D objects quickly turns into a major computational burden. For engineering tasks that involve screening, iteration, or optimization, this repeated-query cost can easily become the main bottleneck.

Our earlier work, GTC-3DEM, showed that a mesh-based deep surrogate could substantially accelerate this stage of the workflow. But that work also made something clear: **for realistic 3D scattering problems, the hard part is not only learning the electromagnetic response, but also learning a transferable understanding of geometry itself**.

## Why Geometry Matters So Much

Electromagnetic scattering is highly sensitive to geometry. Local surface details matter, but so do long-range structural relationships such as wing-body-tail arrangement, component layout, and overall topology. This makes aircraft-level 3D scattering a much more demanding learning problem than low-dimensional parametric regression.

Most existing learning-based surrogates still train geometry encoding and scattering prediction together using the same expensive labeled electromagnetic simulations. That setup works when training and testing data are very similar, but it creates a weakness under out-of-distribution conditions. If the labeled dataset only covers a limited family of target shapes, the model may learn a response predictor that is accurate on familiar geometries yet fragile on unseen aircraft.

This motivated a different question in our new work: **can we learn geometry first, from a cheaper and more general supervisory signal, and only then use expensive electromagnetic labels for downstream adaptation?**

## Our Method: GTC-SDF

The new framework is called **GTC-SDF**, short for Graph-Transformer-Convolutional Signed Distance Function framework.

Its key idea is to split the learning process into two stages:

- Stage 1 learns geometry through self-supervised signed distance field (SDF) reconstruction.
- Stage 2 freezes the pretrained geometry encoder and trains only an electromagnetic decoder for RCS prediction.

The backbone still builds on the mesh-based representation introduced in GTC-3DEM:

- the input object is represented as a triangular surface mesh
- each triangular facet is treated as a graph node
- a graph neural network captures local mesh interactions
- a Transformer models longer-range geometric dependencies
- a convolutional decoder reconstructs the final 2D full-angle RCS map

What changes is the learning strategy. Instead of asking the network to discover geometry only through expensive full-wave labels, **we first train it to understand shape as a continuous implicit field**. Signed distance fields provide dense geometric supervision in continuous space, so the encoder learns shape information that is less tied to one particular mesh discretization and less entangled with one downstream task.

This decoupling is the central idea of the paper. Geometry acquisition and scattering-response learning are no longer forced into the same stage. In our view, that makes the model more aligned with how knowledge should be organized in scientific machine learning: first learn reusable structure, then adapt it to the specific physics task.

## What We Found

The results show that this two-stage strategy works well for aircraft-level 3D PEC electromagnetic scattering.

In Stage 1, the model learns stable geometric latent representations from a large aircraft shape corpus through SDF reconstruction. In Stage 2, those learned geometry features transfer effectively to wideband RCS prediction, even when evaluation is performed under aircraft-level out-of-distribution splits.

Compared with the end-to-end GTC-3DEM baseline, GTC-SDF improves OOD prediction quality across all three reported metrics:

- **PSNR:** from 16.42 to 20.58
- **SSIM:** from 0.7383 to 0.8077
- **MSE:** from 0.0957 to 0.0634

The computational gains are also significant. Total training time drops from **253.69 hours to 53.69 hours**, and the Stage 2 GPU memory requirement decreases from **23,102 MB to 10,648 MB** because only the decoder is optimized during downstream fine-tuning.

This point matters. The contribution of GTC-SDF is not only better accuracy, but also a more efficient training paradigm. The model makes better use of expensive full-wave labels by moving a large part of geometry learning into a label-free pretraining stage.

At the same time, the paper remains careful about scope. The current framework is still limited to PEC targets, still depends on high-quality simulation data for the downstream scattering task, and still does not solve generalization in a universal sense. What it demonstrates is something more specific and more useful: **geometry pretraining is a practical way to improve data efficiency and OOD robustness in 3D electromagnetic surrogate modeling**.

## Why This Matters for Engineering

From an engineering perspective, this work strengthens the case for AI-assisted computational electromagnetics in a very concrete way.

The goal is still not to replace full-wave solvers. Those methods remain essential whenever reliability, interpretability, and physical rigor are non-negotiable. But many engineering pipelines involve repeated evaluations on related but not identical geometries, and this is exactly where learned surrogates can provide real value.

What GTC-SDF suggests is that a good surrogate should not merely memorize response patterns from a fixed labeled dataset. It should build a reusable geometric prior that survives changes in target shape and helps the downstream model adapt under limited supervision. That is especially important for realistic aerospace targets, where unseen aircraft are often the real deployment case rather than the exception.

In this sense, GTC-SDF should be understood as a step from fast prediction toward **knowledge-transfer-oriented surrogate modeling**. It is not just about making inference cheaper. It is about learning geometry in a form that can be reused, transferred, and refined across electromagnetic tasks.

## A Step Further Toward AI4CEM

We view GTC-SDF as a natural continuation of our AI4CEM direction.

GTC-3DEM showed that mesh-based deep learning can directly map 3D geometry to scattering outputs with strong speed advantages. GTC-SDF goes one step further by asking how such a model should be trained if we want better generalization, lower downstream cost, and more reusable geometric knowledge. The answer, at least in this study, is to separate geometry understanding from scattering prediction and to use SDF-based implicit learning as the bridge.

More broadly, this work points toward a future in which AI for computational electromagnetics is not only about fitting faster surrogates, but also about organizing prior knowledge more effectively. Better geometric diversity, support for non-PEC materials, stronger cross-domain transfer, and more physics-guided pretraining objectives are all important next directions. But even at this stage, the message is already clear: **AI can help computational electromagnetics not only by accelerating repeated simulation, but by learning reusable geometric knowledge before the expensive electromagnetic task begins**.

<!-- Read our paper for more details: (Waiting for Publication)

Xiaotian Jiang, Hongliang Chen, Huan Huan Zhang, Kaitai Guo, Yang Zheng, Jimin Liang, *SDF-Based Implicit Geometry Pretrained Foundation Model for 3D PEC Electromagnetic Scattering Computation*, 2026. -->

</font>
