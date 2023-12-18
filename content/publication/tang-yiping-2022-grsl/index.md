---
title: Poleward-Motion Aware Network for Poleward Moving Auroral Forms Recognition
authors:
- Yiping Tang
- Kaitai Guo
- Chen Wei
- Yang Zheng
- Shenghan Ren
- Jimin Liang
date: '2022-01-01'
publishDate: '2023-12-18T09:50:18.618300Z'
publication_types:
- article-journal
publication: '*IEEE Geoscience and Remote Sensing Letters*'
doi: 10.1109/LGRS.2022.3147464
abstract: Poleward moving auroral forms (PMAFs) are a common dayside auroral phenomenon,
  and the study of PMAFs has important implications for the exploration of the near-earth
  space physical processes for geosciences. In the all-sky imager (ASI) image sequence,
  PMAFs show a tendency to move northward in the northern hemisphere. Therefore, this
  particular motion pattern can be used for PMAF recognition. Previous works for automatic
  recognition of PMAFs tend to rely on optical flow. However, both the traditional
  and the deep learning-based optical flow estimation methods are time- and memory-expensive.
  In view of the large number of auroral images generated every year, it is impractical
  to estimate the optical flow for all auroral data with limited computational resources.
  In this letter, a poleward-motion aware network (PA-Net) is proposed to extract
  the motion features directly from ASI images. PA-Net computes the correlation between
  each point in an image and the points at the poleward direction in the following
  image by means of a poleward-motion aware operation (PA-Operation), to verify whether
  the point under consideration has undergone poleward motion. In addition, a channel
  attention mechanism is applied to the features obtained by PA-Operation to suppress
  information less helpful for recognizing PMAFs. The PA-Net achieves the best performance
  on the PMAFs recognition dataset over other commonly used action recognition models,
  validating the superiority of our approach. More importantly, the complicated optical
  flow estimation is avoided, making it possible to apply the proposed method to large-scale
  auroral data.
links:
- name: URL
  url: https://ieeexplore.ieee.org/document/9696327
---
