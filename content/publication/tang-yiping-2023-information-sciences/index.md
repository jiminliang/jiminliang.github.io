---
title: Towards better utilization of pseudo labels for weakly supervised temporal
  action localization
authors:
- Yiping Tang
- Junyao Ge
- Kaitai Guo
- Yang Zheng
- Haihong Hu
- Jimin Liang
date: '2023-01-01'
publishDate: '2023-12-18T03:54:34.907364Z'
publication_types:
- article-journal
publication: '*Information Sciences*'
doi: https://doi.org/10.1016/j.ins.2022.12.044
abstract: Weakly supervised temporal action localization (WS-TAL) aims to simultaneously
  recognize and localize action instances of interest in untrimmed videos with the
  use of the video-level label only. Some works have demonstrated that pseudo labels
  play an important role for performance improvement in WS-TAL. Since pseudo labels
  are inevitably inaccurate, direct adoption of noisy labels can lead to inappropriate
  knowledge transfer. Although some previous studies have shown the benefits of using
  only “reliable” pseudo labels, performance improvement is still limited. In this
  work, we experimentally analyze how the noise in pseudo labels affects model performance
  within the self-distillation framework. Motivated by the finding that incorrect
  pseudo labels with large confidence scores have a significant impact on performance,
  we propose the overconfidence suppression (OCS) strategy to mitigate the effect
  of the overconfident pseudo labels, and thus prevent over-fitting of the student
  model. In addition, a simplified contrast learning method is utilized to fine-tune
  the feature representation by increasing the separation of the foreground and background
  snippets. Equipped with the proposed methods, the benefits of pseudo labels can
  be better exploited and allow the model to achieve state-of-the-art performance
  on THUMOS’14 and ActivityNet-1.2 benchmarks.
tags:
- Untrimmed video analysis
- Temporal action detection
- Weakly supervised learning
- Pseudo label
links:
- name: URL
  url: https://www.sciencedirect.com/science/article/pii/S0020025522015390
---
