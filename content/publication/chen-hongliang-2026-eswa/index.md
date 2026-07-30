---
title: Autoregressive Pre-training for Heterogeneous mmWave Radar Perception using
  Mamba
authors:
- Hongliang Chen
- Xiaotian Jiang
- Kaitai Guo
- Yang Zheng
- Siqi Pang
- Shenghan Ren
- Jimin Liang
date: '2026-01-01'
publishDate: '2026-07-30T23:47:37.106002Z'
publication_types:
- article-journal
publication: '*Expert Systems with Applications*, 133829'
pages: '133829'
doi: https://doi.org/10.1016/j.eswa.2026.133829
abstract: 'Public mmWave radar datasets are collected under heterogeneous acquisition
  configurations and processing protocols, leading to systematic geometric and signal-statistical
  shifts across datasets. Even when the underlying hardware is similar, differences
  in grid resolution, field-of-view, measurable range/velocity, and the availability
  of a calibrated Doppler/velocity axis make naive multi-dataset aggregation unreliable
  and can bias models toward dataset-specific artifacts. We propose MetaARM, a metadata-conditioned
  self-supervised pre-training framework for heterogeneous mmWave radar perception.
  MetaARM partitions a 3D radar tensor into non-overlapping 3D patches and trains
  with causal next-patch prediction under a structured serialization order: tokens
  are first ordered along the sequence axis and then raster-scanned within each Range–Azimuth
  plane. To explicitly handle configuration shifts, MetaARM injects acquisition metadata
  through two coupled mechanisms: (i) Absolute Coordinate Encoding (ACE), which converts
  discrete patch indices into normalized physical coordinates using resolution and
  FoV metadata to reduce geometric inconsistency; and (ii) FiLM-based conditioning
  inside Mamba blocks, which calibrates token features before the selective scan according
  to observable acquisition/configuration metadata. Together, these pathways use the
  same metadata to link physical radar-token geometry with configuration-aware sequence
  modeling before autoregressive prediction. Pre-trained on an aggregated corpus of
  five public radar datasets, MetaARM improves transfer performance on three benchmarks,
  achieving 64.5 mAP@0.3 on RADDet, 49.5 mIoU on CARRADA (RA), and 85.0 AP on CRUW,
  improving over matched training-from-scratch, MAE pre-training, joint supervised,
  and lightweight normalization and metadata-affine calibration baselines under the
  reported matched settings. Overall, the results suggest that metadata-conditioned
  autoregressive pre-training is a practical way to learn radar representations that
  transfer better under cross-dataset acquisition/configuration shifts.'
tags:
- millimeter-wave radar
- Self-supervised pre-training
- Autoregressive modeling
- metadata conditioning
links:
- name: URL
  url: https://www.sciencedirect.com/science/article/pii/S0957417426027375
---
