---
title: Discriminative Context-Aware Network for Target Extraction in Remote Sensing
  Imagery
authors:
- Lei Hu
- Chuang Niu
- Shenghan Ren
- Minghao Dong
- Changli Zheng
- Wei Zhang
- Jimin Liang
date: '2022-01-01'
publishDate: '2023-12-18T09:50:18.610726Z'
publication_types:
- article-journal
publication: '*IEEE Journal of Selected Topics in Applied Earth Observations and Remote
  Sensing*'
doi: 10.1109/JSTARS.2021.3138187
abstract: Extracting objects of interest from remote sensing imagery is an essential
  part in various practical applications. The objects that people pay attention to
  in the remote sensing scene mainly include buildings, roads, vehicles, etc. In this
  article, extracting the aforementioned objects are collectively referred to as the
  target extraction task. Arising from object scale variation, appearance similarity
  between adjacent patches, diversity of imaging orientation, and complexity of background,
  it is difficult to extract complete objects from cluttered backgrounds. Deep neural
  network has made great achievement in dense prediction for target extraction. However,
  most of the previous works are still faced with a formidable challenge in discriminative
  context feature representation to extract targets of various categories and correctly
  classify pixels around the boundary. In this article, we propose a target extraction
  neural network, named discriminative context-aware network, to focus on discriminative
  high-level context features and preserve spatial information. First, a discriminative
  context-aware feature module is designed to generate the feature maps in the top
  layer, which not only captures the rich image context information but also aggregates
  the contrasted local information at multiple scales. Second, a refine decoder module
  is adopted to preserve spatial information from low-level layers and enhance the
  feature representation, leading to precise segmentation results. We conducted extensive
  experiments on building and road extraction benchmarks, including WHU building dataset
  and Massachusetts road dataset, together with a self-constructed dataset for vehicle
  extraction in SAR images. Our method achieves state-of-the-art results with fewer
  parameters and faster inference.
links:
- name: URL
  url: https://ieeexplore.ieee.org/document/9663014
---
