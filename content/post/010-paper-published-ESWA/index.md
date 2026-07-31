---
title: "Predicting What Comes Next: Autoregressive Pre-training for Heterogeneous
mmWave Radar Perception"
date: 2026-07-29
image:
  focal_point: 'top'
---

Our paper on autoregressive pre-training for heterogeneous mmWave radar perception has been published by **Expert Systems with Applications** - July 29, 2026.

<!--more-->
---

Our latest paper, *“[Autoregressive Pre-training for Heterogeneous mmWave Radar Perception using Mamba](https://www.sciencedirect.com/science/article/abs/pii/S0957417426027375),”* has been published in *Expert Systems with Applications*.

Pre-training has transformed natural language processing and computer vision. Instead of learning every task from scratch, a model first learns general representations from large amounts of unlabeled data and then adapts them to specific downstream applications. In millimeter-wave (mmWave) radar perception, however, reusable pre-trained models remain surprisingly underexplored. Most radar models are still developed for a single dataset and a single task, despite the growing amount of publicly available radar data.

At first glance, the solution may seem straightforward: combine several public radar datasets and train a larger model. In practice, this is far more difficult than simply increasing the amount of data.

Different radar datasets are collected with different fields of view, measurable ranges, velocity limits, grid resolutions, and signal-processing protocols. Some provide a calibrated Doppler or velocity axis, while others contain only an ordered temporal or sequence dimension. Even after their tensors are resized to the same shape, the same discrete location may represent different physical ranges, angles, or velocities. A model trained by naive data aggregation can therefore mistake differences in sensor configuration for meaningful differences in the scene.

This is the problem we set out to address. In this work, we propose **MetaARM**, a metadata-conditioned autoregressive pre-training framework designed to learn transferable representations from heterogeneous mmWave radar datasets.

The central idea is inspired by one of the most successful learning principles behind modern language models: predicting what comes next. MetaARM divides a three-dimensional radar tensor into non-overlapping patches, arranges them into a structured token sequence, and learns to predict each next radar patch from the preceding context. Unlike masked autoencoding, which reconstructs randomly hidden regions, this causal objective follows the natural ordered structure of radar data. It encourages the model to capture spatial patterns within each Range-Azimuth plane as well as correlations along the Doppler, temporal, or sequence axis.

To model these long radar-token sequences efficiently, we build the encoder with **Mamba**. A radar tensor in our default setting produces 8,192 tokens after patching, making the quadratic cost of Transformer self-attention increasingly restrictive. Mamba's selective state-space mechanism scales linearly with sequence length and naturally matches the causal next-token objective. Importantly, our experiments show that the gain does not come from changing the backbone alone: it emerges from the combination of structured radar tokenization, autoregressive pre-training, and configuration-aware modeling.

Handling dataset heterogeneity is another key part of MetaARM. We use observable acquisition metadata through two complementary pathways. **Absolute Coordinate Encoding (ACE)** maps discrete token indices into normalized physical radar coordinates, reducing geometric inconsistency across sensing configurations. **FiLM-conditioned Mamba** then uses the same metadata to calibrate token features inside each Mamba block before the selective scan. In this way, the model is told not only what a radar signal looks like, but also how and where that signal was measured.

We pre-train MetaARM on an aggregated corpus of five public radar datasets: RADDet, CARRADA, CRUW, SCORP, and RaDICaL. Together, they cover different indoor and outdoor scenes, sensing ranges, resolutions, radar representations, and acquisition configurations. The learned encoder is then transferred to three distinct downstream tasks: 3D object detection on RADDet, semantic segmentation on CARRADA, and keypoint localization on CRUW.

The results consistently support the value of this pre-training strategy. MetaARM achieves 64.5% mAP@0.3 on RADDet, 49.5% Range-Azimuth mIoU on CARRADA, and 85.0% AP on CRUW. Under matched downstream settings, autoregressive pre-training outperforms both training from scratch and MAE pre-training across all three benchmarks. It is particularly valuable when annotations are limited: with only 10% of the RADDet training labels, pre-training improves mAP@0.3 from 12.8% to 21.1%.

The ablation studies also reveal why the framework works. Simply exposing the model to more heterogeneous data through joint supervised training does not reproduce the improvement. Autoregressive pre-training provides a clear advantage over masked autoencoding, while ACE and FiLM offer complementary gains by addressing physical-coordinate inconsistency and configuration-dependent feature shifts. These findings suggest that building a reusable radar model requires more than data scaling alone: the pre-training objective and the physical meaning of heterogeneous sensor data must be considered together.

More broadly, this work is a step toward moving mmWave radar perception from isolated, task-specific models to reusable pre-trained encoders. It shows that the next-token principle behind modern foundation models can also provide a natural learning signal for radar, provided that the geometry and acquisition conditions of different sensors are modeled explicitly. We hope this direction will help unlock the value of existing public radar datasets and support the development of larger, more general radar perception models.

**Reference:** H. Chen, X. Jiang, K. Guo, Y. Zheng, S. Pang, S. Ren, and J. Liang, “Autoregressive Pre-training for Heterogeneous mmWave Radar Perception using Mamba,” *Expert Systems with Applications*, article 133829, 2026. [https://doi.org/10.1016/j.eswa.2026.133829](https://doi.org/10.1016/j.eswa.2026.133829).
