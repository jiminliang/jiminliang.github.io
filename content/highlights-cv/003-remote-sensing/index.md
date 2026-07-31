---
title: Remote Sensing Image Analysis
date: 2026-04-25
aliases:
  - /highlights-cv/003-rsteller/
  - /highlights-cv/004-thinkrs/
image:
  focal_point: 'top'
---

We develop LLM- and VLM-driven methods to make remote sensing image analysis more scalable, semantically rich, and capable of reasoning. Our work spans large-scale vision-language data construction and reasoning-driven pixel-level understanding, connecting open geospatial data, language models, and universal segmentation models.

<!--more-->

<font size=3>

## Research Projects

- [**RSTeller: Scaling Vision-Language Learning with Open Geospatial Data**](#rsteller-scaling-vision-language-learning-with-open-geospatial-data)
- [**Think2Seg-RS: From Semantic Reasoning to Pixel-Level Delineation**](#think2seg-rs-from-semantic-reasoning-to-pixel-level-delineation)

Our research explores how large language models (LLMs) and vision-language models (VLMs) can make remote sensing systems more scalable, accessible, and capable of understanding complex geospatial scenes. The two projects below address complementary parts of this goal. RSTeller expands the visual-language knowledge available for remote sensing by transforming open geospatial resources into large-scale, semantically rich training data. Think2Seg-RS then investigates how high-level visual-language reasoning can be translated into precise spatial actions at the pixel level. Together, they trace a path from building domain knowledge at scale to using that knowledge for reasoning-driven image analysis.

## RSTeller: Scaling Vision-Language Learning with Open Geospatial Data

[*Paper*](https://www.sciencedirect.com/science/article/pii/S0924271625001832) · [*Dataset and code*](https://github.com/SlytherinGe/RSTeller)

Modern VLMs learn powerful associations between images and language from enormous collections of image-text pairs. Remote sensing, however, lacks comparably large and richly described public datasets. Existing datasets are often limited in scale, while manually writing detailed captions for aerial imagery requires substantial time and domain expertise. This data bottleneck makes it difficult to scale remote sensing VLMs and limits their ability to interpret complex scenes in natural language.

To address this problem, we developed **RSTeller**, an automated workflow for constructing remote sensing image-text data from openly available geospatial resources. Google Earth Engine provides large-scale aerial imagery, OpenStreetMap supplies geographically aligned semantic information, and open-source LLMs interpret structured OSM tags and turn them into fluent descriptions. The workflow covers data acquisition, LLM-based caption generation and augmentation, quality control, and final dataset compilation, making the process reproducible and extensible to larger or more diverse data sources.

{{< figure src="overall_workflow.jpg" caption="The RSTeller data-generation workflow combines remote sensing imagery from Google Earth Engine, geospatial semantics from OpenStreetMap, and LLM-based caption generation." >}}

Using this workflow, we created a dataset of more than **1.3 million remote sensing images**, each paired with two descriptive captions, resulting in approximately **2.6 million image-text pairs**. The captions describe both area elements, such as land-use regions and buildings, and non-area elements, such as roads and rivers. Caption augmentation further increases linguistic diversity. Measured by the MTLD lexical-diversity score, RSTeller's captions are more than twice as diverse as those of the next most linguistically varied dataset in the paper's comparison.

{{< figure src="dataset_comparison.jpg" caption="Comparison of the scale and linguistic diversity of remote sensing image-text datasets. RSTeller combines a large number of image-text pairs with rich caption semantics." >}}

We evaluated RSTeller by continually pre-training multiple CLIP-based VLMs and testing them on zero-shot remote sensing scene classification and image-text retrieval. The results show consistent improvements across model sizes and downstream benchmarks. The experiments also reveal several practical lessons: mixing general-domain data with remote sensing data helps preserve broad visual knowledge, LLM-generated descriptions are more effective than simple tag templates, and increasing the amount of domain data generally continues to improve performance. These findings demonstrate that both data scale and linguistic quality matter when adapting VLMs to remote sensing.

The broader contribution of RSTeller is therefore not only a new dataset, but also a scalable way to turn abundant open imagery and geographic metadata into useful multimodal supervision. By reducing the dependence on manual captioning and releasing the data-generation resources publicly, this work lowers the barrier to developing stronger and more accessible remote sensing VLMs.

**Reference:** Junyao Ge, Xu Zhang, Yang Zheng, Kaitai Guo, Jimin Liang*, [RSTeller: Scaling up visual language modeling in remote sensing with rich linguistic semantics from openly available data and large language models](https://doi.org/10.1016/j.isprsjprs.2025.05.002), *ISPRS Journal of Photogrammetry and Remote Sensing*, 226: 146-163, 2025.

## Think2Seg-RS: From Semantic Reasoning to Pixel-Level Delineation

[*Paper*](https://www.sciencedirect.com/science/article/pii/S0924271626002091)

Most remote sensing segmentation systems assume that the target is stated explicitly: a building, a road, a vehicle, or another category with recognizable visual attributes. Real geospatial questions are often less direct. A user may ask for *the sports area most suitable for hurdle racing* or *the facility that should be monitored for hazardous leaks*. Answering such queries requires the model to infer an implicit concept or function before locating the corresponding regions. This emerging task, known as **reasoning segmentation**, connects high-level semantic reasoning with precise pixel-level delineation.

We proposed **Think2Seg-RS** to bridge these two very different capabilities through a decoupled reasoning-execution design. A trainable large vision-language model interprets the remote sensing image and query, produces a reasoning trace, and converts its conclusion into structured geometric prompts consisting of bounding boxes and positive points. A frozen SAM2 model then executes those prompts to generate the segmentation mask. The LVLM is responsible for understanding *what* the query means and *where* the relevant regions should be, while SAM2 remains a reusable engine for determining the exact pixel boundaries.

{{< figure src="think2seg-rs-framework.jpg" caption="Think2Seg-RS separates semantic reasoning from segmentation execution. An LVLM generates structured geometric prompts, and a frozen SAM2 model converts them into masks; mask-level feedback is used to optimize the prompting policy." >}}

A central challenge is learning prompts without imposing a single handcrafted box-point target. Many different prompt configurations can lead SAM to the same correct mask, so imitating pseudo prompts can unnecessarily restrict the model and introduce biases from intermediate annotations. Think2Seg-RS instead uses a **mask-only Group Relative Policy Optimization (GRPO)** objective. The LVLM is rewarded for producing a valid structured response and for the IoU of the final SAM-generated mask. Training therefore evaluates whether the reasoning ultimately leads to the right segmentation result, without requiring pseudo box-point supervision.

Think2Seg-RS achieves state-of-the-art performance on the EarthReason benchmark, reaching **75.60% cIoU** and **73.36% gIoU** on the test set. It also exhibits strong zero-shot transfer to remote sensing referring-segmentation benchmarks, showing that the learned reasoning-to-prompt policy generalizes beyond the training queries and dataset. These results support the value of directly connecting semantic reasoning to spatial execution through final-mask feedback.

The experiments also expose important distinctions between semantic-level and instance-level grounding. Semantic reasoning may require aggregating all regions that satisfy a concept, whereas instance-level benchmarks require individual objects to remain separated. Under semantic-level supervision, compact SAM2 variants can outperform larger ones because they are less prone to fragmenting a coherent semantic region according to local texture. Negative points, although useful in interactive segmentation, are also difficult to optimize reliably in heterogeneous aerial backgrounds. These observations suggest that model scale and prompting strategies must be aligned with annotation granularity rather than chosen in isolation.

More broadly, Think2Seg-RS moves remote sensing analysis beyond recognizing explicitly named objects. By allowing a system to interpret concepts, functions, and geospatial relationships before delineating the relevant regions, it offers a modular route toward remote sensing models that can respond to more natural and demanding human queries.

**Reference:** Xu Zhang, Junyao Ge, Yang Zheng, Kaitai Guo, Jimin Liang*, [Bridging semantics and geometry: A decoupled LVLM-SAM framework for reasoning segmentation in optical remote sensing](https://doi.org/10.1016/j.isprsjprs.2026.04.036), *ISPRS Journal of Photogrammetry and Remote Sensing*, 237: 217-235, 2026.

</font>
