---
title: Millimeter-Wave Radar Perception
date: 2026-07-29
image:
  focal_point: 'top'
---

We develop learning-based methods for environment perception from millimeter-wave radar imaging, with an emphasis on physics-aware representation learning, scalable pre-training, and language-guided open-world understanding. Our goal is to turn rich radar spectrum measurements into robust, transferable, and queryable representations for object detection and scene understanding under challenging sensing conditions.

<!--more-->

<font size=3>

## Research Projects

- [**MetaARM: Autoregressive Pre-training for Heterogeneous Radar Perception**](#metaarm-autoregressive-pre-training-for-heterogeneous-radar-perception)

Millimeter-wave (mmWave) radar provides a distinctive view of the environment. It directly measures range, azimuth, and radial motion, operates without external illumination, and remains comparatively robust when darkness, adverse weather, or partial occlusion degrades optical sensing. These properties make radar an important source of complementary information and safety redundancy for intelligent vehicles and other autonomous systems.

Our research focuses on learning directly from dense radar spectra and tensors, which preserve substantially more echo information than sparse point clouds produced after thresholding, peak detection, clustering, and tracking. Making effective use of these measurements is challenging. The Range, Azimuth, and Doppler axes arise from different physical mechanisms and exhibit strong anisotropy; signal statistics and spatial resolution change with radar coordinates; and public datasets differ in sensing range, field of view, resolution, and tensor construction. Radar measurements also lack the high-level semantics needed for natural-language interaction and open-world understanding.

We investigate these challenges across several connected directions: physics-aware encoders that respect the native structure of radar data, scalable pre-training across heterogeneous sensing configurations, stronger object detection and scene understanding, multimodal alignment among images, radar, and language, and reliable perception under interference and uncertainty. The project below presents our first step toward reusable pre-trained representations for this broader radar perception framework.

## MetaARM: Autoregressive Pre-training for Heterogeneous Radar Perception

[*Paper*](https://www.sciencedirect.com/science/article/abs/pii/S0957417426027375) · [*DOI*](https://doi.org/10.1016/j.eswa.2026.133829)

Pre-training has become a standard way to learn transferable representations from large unlabeled corpora in language and vision. In mmWave radar perception, however, reusable pre-trained models remain relatively uncommon. Radar annotations are expensive, individual public datasets are limited in scale and scene coverage, and most existing systems are trained for a single task on a single acquisition setup. These limitations leave a large amount of unlabeled radar data underused.

Combining public datasets is not as simple as resizing their tensors and training on the resulting mixture. Radar datasets are collected with different fields of view, measurable ranges and velocities, grid resolutions, and signal-processing protocols. Some provide a calibrated Doppler or velocity axis, while others contain only an ordered temporal or sequence dimension. Consequently, even after resampling to a common tensor size, the same discrete index can represent different physical positions or velocities. Naive aggregation can therefore encourage a model to learn dataset-specific acquisition artifacts rather than transferable scene structure.

To address this problem, we developed **MetaARM**, a metadata-conditioned autoregressive pre-training framework for heterogeneous mmWave radar perception. MetaARM divides a three-dimensional radar tensor into non-overlapping patches and serializes them with a structured order: tokens first follow the sequence axis and are then raster-scanned within each Range-Azimuth plane. Instead of reconstructing randomly masked regions as in MAE, the model learns through **causal next-patch prediction**, using preceding radar tokens to predict the raw signal of the next patch.

The encoder is built with **Mamba**, whose selective state-space mechanism scales linearly with sequence length and is well suited to the long token sequences produced by dense three-dimensional radar tensors. This architecture matches the causal pre-training objective while allowing the model to capture both spatial structure within Range-Azimuth planes and correlations across Doppler, temporal, or other ordered sequence dimensions.

{{< figure src="metaarm-framework.png" caption="The MetaARM framework combines structured radar-patch ordering, Absolute Coordinate Encoding (ACE), a metadata-conditioned Mamba encoder, and causal next-token prediction to learn transferable representations from heterogeneous radar tensors." >}}

Acquisition metadata enters MetaARM through two complementary pathways. **Absolute Coordinate Encoding (ACE)** converts discrete patch indices into normalized physical radar coordinates, reducing the geometric inconsistency caused by different grid resolutions and sensing extents. **FiLM conditioning** uses observable configuration metadata, including field of view, measurable range, resolution, and Doppler availability, to calibrate features inside each Mamba block before the selective scan. Together, these mechanisms turn dataset configuration differences from an uncontrolled source of bias into an explicit condition for representation learning.

We pre-trained MetaARM on an aggregated corpus of five public radar datasets: RADDet, CARRADA, CRUW, SCORP, and RaDICaL. The learned encoder was then transferred to three different downstream tasks: 3D object detection on RADDet, semantic segmentation on CARRADA, and keypoint localization on CRUW. This design tests whether the representation transfers not only across acquisition configurations, but also across perception tasks and output formats.

MetaARM achieves **64.5% mAP@0.3** on RADDet, **49.5% Range-Azimuth mIoU** on CARRADA, and **85.0% AP** on CRUW. Under matched downstream settings, autoregressive pre-training consistently outperforms training from scratch, MAE pre-training, and joint supervised training. The benefit is especially pronounced when annotations are scarce: using only 10% of the RADDet labels, pre-training improves mAP@0.3 from 12.8% to 21.1%. These results suggest that metadata-conditioned next-token prediction is a practical route toward reusable radar encoders that can learn from otherwise incompatible public data sources.

**Reference:** H. Chen, X. Jiang, K. Guo, Y. Zheng, S. Pang, S. Ren, and J. Liang, [“Autoregressive Pre-training for Heterogeneous mmWave Radar Perception using Mamba,”](https://www.sciencedirect.com/science/article/abs/pii/S0957417426027375) *Expert Systems with Applications*, article 133829, 2026. [https://doi.org/10.1016/j.eswa.2026.133829](https://doi.org/10.1016/j.eswa.2026.133829).

## Research Outlook

Our ongoing research explores radar-native representation learning that better reflects physical coordinates and axis-specific structure, stronger detection and perception in complex scenes, open-world querying and target localization through the joint use of images, mmWave radar, and language, and trustworthy sensing under interference and uncertainty. Together, these directions aim to move radar perception from isolated task-specific detectors toward adaptable systems that can learn across configurations, interact through semantic queries, and communicate when their outputs are reliable.

</font>
