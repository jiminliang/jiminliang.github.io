---
title: 'NPENAS: Neural Predictor Guided Evolution for Neural Architecture Search'
authors:
- Chen Wei
- Chuang Niu
- Yiping Tang
- Yue Wang
- Haihong Hu
- Jimin Liang
date: '2023-01-01'
publishDate: '2023-12-18T09:50:18.557720Z'
publication_types:
- article-journal
publication: '*IEEE Transactions on Neural Networks and Learning Systems*'
doi: 10.1109/TNNLS.2022.3151160
abstract: Neural architecture search (NAS) adopts a search strategy to explore the
  predefined search space to find superior architecture with the minimum searching
  costs. Bayesian optimization (BO) and evolutionary algorithms (EA) are two commonly
  used search strategies, but they suffer from being computationally expensive, challenging
  to implement, and exhibiting inefficient exploration ability. In this article, we
  propose a neural predictor guided EA to enhance the exploration ability of EA for
  NAS (NPENAS) and design two kinds of neural predictors. The first predictor is a
  BO acquisition function for which we design a graph-based uncertainty estimation
  network as the surrogate model. The second predictor is a graph-based neural network
  that directly predicts the performance of the input neural architecture. The NPENAS
  using the two neural predictors are denoted as NPENAS-BO and NPENAS-NP, respectively.
  In addition, we introduce a new random architecture sampling method to overcome
  the drawbacks of the existing sampling method. Experimental results on five NAS
  search spaces indicate that NPENAS-BO and NPENAS-NP outperform most existing NAS
  algorithms, with NPENAS-NP achieving state-of-the-art performance on four of the
  five search spaces.
links:
- name: URL
  url: https://ieeexplore.ieee.org/document/9723446
---
