---
title: 'DERE-Net: A dual-encoder residual enhanced U-Net for muscle fiber segmentation
  of H&E images'
authors:
- Getao Du
- Peng Zhang
- Jianzhong Guo
- Xu Zhou
- Guanghan Kan
- Jiajie Jia
- Jimin Liang
- Xiaoping Chen
- Yonghua Zhan
date: '2024-01-01'
publishDate: '2024-08-15T01:27:51.862198Z'
publication_types:
- article-journal
publication: '*Biomedical Signal Processing and Control*'
doi: https://doi.org/10.1016/j.bspc.2024.106765
abstract: Accurate segmentation of hematoxylin-eosin (H&E) muscle fiber images is
  crucial for the diagnosis of weightless muscle atrophy. However, uneven contrast,
  blurred fiber boundaries and adhesions in H&E images are still challenges for accurate
  segment complete muscle fiber. Although the existing single-encoder based U-shaped
  networks can extract local information about the target in H&E images, ignores remote
  dependencies between muscle fibers and low-level detail features, resulting in poor
  segmentation accuracy when facing H&E images with complex contrast. Therefore, we
  propose a dual-encoder residual enhanced U-Net segmentation model (DERE-Net) for
  effective segment muscle fibers in H&E images. DERE-Net uses Transformer and residual
  CNN to extract global context information and local features of muscle fibers in
  parallel, and fuses these two features to enable the model to accurately identify
  the muscle fibers. The multi-scale semantic information fusion (MSIF) module also
  utilizes the differences between multi-scale features to recover undetected muscle
  fiber, thus improving the network’s ability to recognize the object regions. In
  addition, the attention module is added to the skip connection, making the muscle
  fiber regions information more prominent and improving the robustness of the model.
  To demonstrate the DERE-Net effect, the comparative experiments are conducted on
  our own muscle fiber H&E image dataset, GLAS and MoNuSeg. DERE-Net achieved excellent
  performance on the muscle fiber H&E dataset (DSC 0.919), GLAS dataset (DSC 0.912),
  and MoNuSeg dataset (DSC 0.821). These results indicate that DERE-Net can accurately
  predict muscle fiber regions, providing a new method for accurate diagnosis of muscle
  atrophy in the future.
tags:
- Muscle fiber segmentation
- H&E images
- Deep learning
- Dual-encoder branches
- MSIF module
links:
- name: URL
  url: https://www.sciencedirect.com/science/article/pii/S1746809424008231
---
