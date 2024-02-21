---
title: 'GATCluster: Self-supervised Gaussian-Attention Network for Image Clustering'
authors:
- Chuang Niu
- Jun Zhang
- Ge Wang
- Jimin Liang
date: '2020-01-01'
publishDate: '2024-02-21T10:13:30.789644Z'
publication_types:
- paper-conference
publication: '*Computer Vision -- ECCV 2020*'
abstract: We propose a self-supervised Gaussian ATtention network for image Clustering
  (GATCluster). Rather than extracting intermediate features first and then performing
  traditional clustering algorithms, GATCluster directly outputs semantic cluster
  labels without further post-processing. We give a Label Feature Theorem to guarantee
  that the learned features are one-hot encoded vectors and the trivial solutions
  are avoided. Based on this theorem, we design four self-learning tasks with the
  constraints of transformation invariance, separability maximization, entropy analysis,
  and attention mapping. Specifically, the transformation invariance and separability
  maximization tasks learn the relations between samples. The entropy analysis task
  aims to avoid trivial solutions. To capture the object-oriented semantics, we design
  a self-supervised attention mechanism that includes a Gaussian attention module
  and a soft-attention loss. Moreover, we design a two-step learning algorithm that
  is memory-efficient for clustering large-size images. Extensive experiments demonstrate
  the superiority of our proposed method in comparison with the state-of-the-art image
  clustering benchmarks.
links:
- name: URL
  url: https://link.springer.com/chapter/10.1007/978-3-030-58595-2_44
---
