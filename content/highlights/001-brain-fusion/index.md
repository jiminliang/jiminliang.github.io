---
title: Brain-machine fusion - From brain-in-the-loop to brain-out-of-the-loop
date: 2023-12-20
# image:
#   focal_point: 'top'
---

We proposed a brain-machine fusion approach to achieve the brain-in-the-loop modeling and brain-out-of-the-loop application.

<!--more-->

{{< spoiler text="**Introduction**" >}}
Harnessing the complementarity between the brain and artificial neural networks has shown great promise for the development of novel brain-machine fusion systems that may rival the robustness and flexibility of the human visual system. Nonetheless, due to the requirement of human involvement, brain-machine fusion models are challenging to apply in a brain-in-the-loop manner to handle task demands that involve long duration, high intensity and complex operating environments. To tackle this problem, we proposed a brain-machine fusion approach to achieve the brain-in-the-loop modeling and brain-out-of-the-loop application. The similarities and differences between the image representations of brain responses and image features computed by deep convolutional neural network (DCNN) are firstly analyzed using a rhesus monkey dataset, and the results lay the foundation for the feasibility of brain-machine fusion. A brain-machine fusion model is then developed and a multimodal supervised contrastive learning method is proposed to jointly learn the image representations for brain responses and DCNNs. The fusion model can be applied in a brain-out-of-the-loop manner, effectively addressing the challenges encountered by human-involved approaches. Extensive experiments on a self-built human vehicle detection dataset demonstrate the effectiveness of the proposed method in improving the generalization ability of the downstream image classifiers, both in cross-modal learning or multimodal fusion settings. 

{{< figure src="Fig2.png" id="diagram" >}}
<!-- The figure can now be cross-referenced with a link in the form [A Figure](#figure-hello) -->
{{< /spoiler >}}

{{< spoiler text="**Datasets**" >}}
Two datasets were used in this study. A rhesus monkey dataset was used for complementary analysis between the brain responses and the DCNN image features, and a self-built human vehicle detection dataset was used for brain-image fusion modeling and application in real scenarios.

- Rhesus monkey dataset

The rhesus monkey dataset is obtained from the [Brain-Score platform](https://www.brain-score.org/) including both the stimulus images and EEG brain responses. The stimulus images were synthesised artificially by overlapping the two-dimensional (2D) projections of three-dimensional (3D) objects on random backgrounds. There are 8 object categories, where each category contains 8 subcategories, 50 images per subcategory, for a total of 3200 images. The EEG brain responses were collected from the visual cortex ventral stream region of two trained adult rhesus monkeys, by implanting 168 and 128 (publicly available data only 88) electrodes in the inferior temporal lobe (IT) and V4, respectively. For brain responses acquisition, groups of 5-10 stimulus images were presented sequentially with each image presenting for 100 ms, followed by a 100 ms blank to keep the monkeys focused. Each stimulus image was presented at least 28 times, with an average of 50 times. The publicly available brain responses from the Brain-Score platform were averaged in both the dimension of image presentation times and brain responses time for 70-170 ms after presentation. Thus, the EEG brain responses of IT and V4 are 168- and 88-dimensional vectors respectively, in which each vector element represents the averaged brain response intensity of an electrode.

- Self-built human vehicle detection dataset

Visual stimulus images for the vehicle detection experiment were collected from the VEDAI dataset in the publicly available [Utah AGRC database](http://gis.utah.gov/). In order to exclude the influence of color, we only used large-size (1,024 × 1,024 pixel$^{2}$) infrared image in this study. From the infrared images, we manually cropped patches containing at least two vehicles and of similar size. Totally 2,030 patches (1,015 target patches and 1,015 non-target patches) were obtained, and then resized to 300 ×300 pixel$^{2}$. Considering that the patches were designed to be viewed by human subjects, the scene complexity was first visually inspected based on the type, number, distribution, and similarity of background items. Patches with high confidence were assigned to the simple or complex group, while other indistinguishable patches were excluded. Thereafter, quantitative evaluation in terms of brightness and scene complexity was performed for each patch. The brightness was measured as the average intensity, and the scene complexity was measured by information entropy and gray-level homogeneity indices. Outliers exceeding 1.5 times the interquartile range of these measure were sequentially excluded from the stimulus set. 

The above screening procedure eventually yielded 1800 patches, including 450 patches of each of the four types: simple scene with vehicle (simple-scene target), simple scene without vehicle (simple-scene non-target), complex scene with vehicle (complex-scene target), and complex scene without vehicle (complex-scene non-target).

The experiment comprised two vehicle detection tasks respectively in simple scene and complex scene, totally lasted two hours including preparation work. The experimental paradigm is illustrated in [Fig. 1](#figure-Fig1). During the experiment, the participants were cued to perform a practicing block to adapt to the experimental environment and familiar with the experimental process before the experiment officially began. For each of the two tasks, 900 visual stimulus images containing two categories (450 targets and 450 non-targets) were partitioned into 30 sets of 30 images each for block design. In one block, the set of 30 images contained approximately 40\% to 60\% target images and were randomly permuted. The order of the blocks was also randomly permuted. The participants were asked to fully focus on vehicle detection when the monitor flashed the images of each stimulus for a period of 0.75 second during each block. A black crosshair was displayed in the center of the monitor for 0.75–1 second as the inter-stimulus interval between two adjacent images. At the end of each block, the participants made keystroke judgments about the number of target patches in the block. 

We acquired continuous EEG data using an ActiCHamp EEG system supplied by the Brain Products Company. Sixty-four channels including one reference channel (channel Iz) were positioned on the head according to the international standard 10-10 system. The EEG data were sampled at a rate of 1,000 Hz and the impedance of each electrode was kept below 5 k$\Omega$ prior to the beginning of recording. The raw EEG data were preprocessed offline in MATLAB using the EEGLAB toolbox (version 13.6.5b).


{{< figure src="Fig1.png" id="Fig1" >}}
<!-- The figure can now be cross-referenced with a link in the form [A Figure](#figure-hello) -->
Fig. 1. Left: the generation of stimulus set and statistical results between targets (T) and non-target (nT) stimuli in simple and complex scene groups. Right: the temporal structure of stimulus presentation. Both simple and complex stimulus task shared the same experimental procedure.

{{< /spoiler >}}
