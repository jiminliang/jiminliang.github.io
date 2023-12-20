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


<!-- ------------------------------------------------------- -->
{{< spoiler text="**Datasets**" >}}
Two datasets were used in this study. A rhesus monkey dataset was used for complementary analysis between the brain responses and the DCNN image features, and a self-built human vehicle detection dataset was used for brain-image fusion modeling and application in real scenarios.

- Rhesus monkey dataset

The rhesus monkey dataset is obtained from the [Brain-Score platform](https://www.brain-score.org/) including both the stimulus images and EEG brain responses. The stimulus images were synthesised artificially by overlapping the two-dimensional (2D) projections of three-dimensional (3D) objects on random backgrounds. There are 8 object categories, where each category contains 8 subcategories, 50 images per subcategory, for a total of 3200 images. The EEG brain responses were collected from the visual cortex ventral stream region of two trained adult rhesus monkeys, by implanting 168 and 128 (publicly available data only 88) electrodes in the inferior temporal lobe (IT) and V4, respectively. For brain responses acquisition, groups of 5-10 stimulus images were presented sequentially with each image presenting for 100 ms, followed by a 100 ms blank to keep the monkeys focused. Each stimulus image was presented at least 28 times, with an average of 50 times. The publicly available brain responses from the Brain-Score platform were averaged in both the dimension of image presentation times and brain responses time for 70-170 ms after presentation. Thus, the EEG brain responses of IT and V4 are 168- and 88-dimensional vectors respectively, in which each vector element represents the averaged brain response intensity of an electrode.

- Self-built human vehicle detection dataset

Visual stimulus images for the vehicle detection experiment were collected from the VEDAI dataset in the publicly available [Utah AGRC database](http://gis.utah.gov/). In order to exclude the influence of color, we only used large-size (1,024 × 1,024 pixel$^{2}$) infrared image in this study. From the infrared images, we manually cropped patches containing at least two vehicles and of similar size. Totally 2,030 patches (1,015 target patches and 1,015 non-target patches) were obtained, and then resized to 300 ×300 pixel$^{2}$. Considering that the patches were designed to be viewed by human subjects, the scene complexity was first visually inspected based on the type, number, distribution, and similarity of background items. Patches with high confidence were assigned to the simple or complex group, while other indistinguishable patches were excluded. Thereafter, quantitative evaluation in terms of brightness and scene complexity was performed for each patch. The brightness was measured as the average intensity, and the scene complexity was measured by information entropy and gray-level homogeneity indices. Outliers exceeding 1.5 times the interquartile range of these measure were sequentially excluded from the stimulus set. 

The above screening procedure eventually yielded 1800 patches, including 450 patches of each of the four types: simple scene with vehicle (simple-scene target), simple scene without vehicle (simple-scene non-target), complex scene with vehicle (complex-scene target), and complex scene without vehicle (complex-scene non-target).

The experiment comprised two vehicle detection tasks respectively in simple scene and complex scene, totally lasted two hours including preparation work. During the experiment, the participants were cued to perform a practicing block to adapt to the experimental environment and familiar with the experimental process before the experiment officially began. For each of the two tasks, 900 visual stimulus images containing two categories (450 targets and 450 non-targets) were partitioned into 30 sets of 30 images each for block design. In one block, the set of 30 images contained approximately 40\% to 60\% target images and were randomly permuted. The order of the blocks was also randomly permuted. The participants were asked to fully focus on vehicle detection when the monitor flashed the images of each stimulus for a period of 0.75 second during each block. A black crosshair was displayed in the center of the monitor for 0.75–1 second as the inter-stimulus interval between two adjacent images. At the end of each block, the participants made keystroke judgments about the number of target patches in the block. 

We acquired continuous EEG data using an ActiCHamp EEG system supplied by the Brain Products Company. Sixty-four channels including one reference channel (channel Iz) were positioned on the head according to the international standard 10-10 system. The EEG data were sampled at a rate of 1,000 Hz and the impedance of each electrode was kept below 5 k$\Omega$ prior to the beginning of recording. The raw EEG data were preprocessed offline in MATLAB using the EEGLAB toolbox (version 13.6.5b).


{{< figure src="Fig1.png" id="Fig1" >}}
<!-- The figure can now be cross-referenced with a link in the form [A Figure](#figure-hello) -->
Fig. 1. Left: the generation of stimulus set and statistical results between targets (T) and non-target (nT) stimuli in simple and complex scene groups. Right: the temporal structure of stimulus presentation. Both simple and complex stimulus task shared the same experimental procedure.

<!-- The experimental paradigm is illustrated in [Fig. 1](#figure-Fig1). -->

{{< /spoiler >}}

<!-- ------------------------------------------------------- -->

{{< spoiler text="**Complementarity between the image representations of brain and DCNN**" >}}

- Methods

The rhesus monkey dataset was used for complementary analysis between the brain responses and the DCNN image features. We employed the representational similarity analysis (RSA) method to analyze the similarity between the brain responses and the DCNN features. The basis of RSA is the representational dissimilarity matrices (RDMs), and we calculated the RDMs for brain responses and DCNN features separately using the Euclidean distance. Specifically, the RDMs were calculated from three levels of granularity, including the image level (RDM shape of 3200 × 3200), the object (subclass) level (RDM shape of 64 × 64), and the class level (RDM shape of 8 × 8). The similarities between the RDMs were then evaluated using Spearman's correlation, and the retest consistency of brain responses between the multiple presentations of the same stimulus image at different levels was used as the noise-limited upper bound.

To investigate the capacity of DCNN features to fit the brain responses, the partial least squares (PLS) was used to predict the brain responses of individual electrodes from the image features.

To investigate whether the differences in the image representations of brain responses and DCNN features are related to image complexity, we used the classification sensitivity index ($d^{'}$) in Rajalingham et. al. (Journal of Neuroscience 38(33), 2018) to estimate the sample separability in different feature spaces. The higher the sensitivity index, the better the separability. The sensitivity indices of the brain responses and DCNN features for each stimulus image were computed separately. 

{{< figure src="Fig3.png" id="diagram" >}}
Fig. 2. Complementarity analysis between the image representations of brain responses and DCNNs. (A) Visualization of RDMs at different levels of classification granularity, and similarity between the RDMs of the brain responses and the DCNN image features. V4 Consistency and IT Consistency represent the retest consistencies of V4 and IT brain responses, respectively. (B) Fitting ability of V4 brain responses and DCNN features to predict the IT responses. (C) Effects of object and scene complexity on classification performance (averaged sensitivity indices) of the brain responses and DCNN features for all stimulus images.

- Results

We found that the brain responses in the primate ventral visual pathway and the DCNN-based visual features show high similarity at the object and class levels, while significant differences existed at the image level. This is consistent with previous behavioural previous studies on DCNN and primate image classification, in which they found that DCNN could accurately predict the primate's classification patterns at the object level, but hardly at the image level. It can therefore be inferred that the DCNN models can be compared to primate vision at coarse-grained object level and class level, but cannot fully account for the fine-grained image-level representations. When using the V4 responses and DCNN features to predict the IT responses, our results indicated that the shallow DCNNs (AlexNet and VGG) could capture more information about IT responses than the deeper DCNNs (GoogLeNet and ResNet), but neither V4 nor various DCNNs could fully represent the IT brain responses. Furthermore, we found that V4 response and DCNN features captured different aspects of IT response information, while all DCNN features mostly captured the similar aspects. These results suggest that DCNN features cannot fully account for the image representation information of the brain responses, but encode the high-level semantic information of the image in a different way. This complementary between DCNN and brain representations highlights the promising potential and practical value of constructing brain-machine fusion models.

Notably, we found that the shallow DCNNs are better at capturing the IT response information than the deeper models, contrary to the previous behavioural study. This inconsistency can be explained in two ways: (1) The localized brain responses of the IT region do not fully reflect the information processing in which multiple regions of the brain are involved. (2) The lack of temporal information in the IT response data cannot reflect the dynamic process of visual processing on time scales and may reduce the brain's representational capacity. Due to the above limitations, the brain responses in the rhesus monkey dataset can only partially reflect the object recognition ability in primates, which is insufficient to form a complete semantic representation of the stimulus images. 

{{< /spoiler >}}