---
title: Cognitive training - Exercise your brain like a muscle
date: 2023-12-18
image:
  focal_point: 'top'
---

Boosting brain-computer interface performance through cognitive training: a brain-centric approach

<!--more-->

<font size=3>

**Introduction**

Previous efforts to boost brain-computer interface (BCI) performance have predominantly focused on optimizing brain signal decoding algorithms. However, the untapped potential of leveraging brain plasticity for optimization remains underexplored. In this study, we aimed to enhance the temporal resolution of the human brain in discriminating visual stimuli by eliminating attentional blink (AB) through color-salient cognitive training, and confirmed that the mechanism is an attention-based improvement. Using the rapid serial visual presentation (RSVP)-based BCI, we evaluated the behavioral and electroencephalogram (EEG) decoding performance of subjects before and after cognitive training in high target percentage (with AB) and low target percentage (without AB) surveillance tasks, respectively. The results consistently demonstrated significant improvement among trained subjects. Further analysis indicated that this improvement was attributed to the fact that the cognitively trained brain could produce more discriminative EEG. Our work highlights the feasibility of cognitive training as a means of brain enhancement for boosting BCI performance.

**Methods**

Utilizing a repeated measures design, we randomly allocated subjects to either the experimental group (group A) or the passive control group (group B), and trained group A for 3 days employing the same color-salient cognitive training task (Fig. 1a) as described by Choi et al. (Proc. Natl. Acad. Sci. 109, 12242–12247, 2012). We evaluated the differences between the pre-test and post-test in the two groups across three tasks. Specifically, first, we employed an AB task (Fig. 1b) to ascertain whether training could eliminate AB, validating Choi's neural mechanism explanation by use of high temporal resolution event-related potential (ERP). Second, we introduced a high-target-percentage surveillance (HTPS) task (Fig. 1c) wherein AB is inevitable. Our hypothesis posited that trained subjects would show superior performance in the HTPS task because targets presented within the AB window convert from being "unseen" to "seen", which would alleviate the high FN during EEG decoding. In addition, we incorporated a low-target-percentage surveillance (LTPS) task (Fig. 1d) in which AB would never occur. We hypothesized that trained subjects would also exhibit superior performance in the LTPS task. We anticipated that their brains possessed exceptional attention and could generate more discriminative target/non-target EEG, consequently alleviating the high false positives (FP) during EEG decoding. To the best of our knowledge, this is the first study in the BCI field that improves system performance by optimizing brain signals, as opposed to focusing on EEG decoding algorithms.

{{< figure src="Fig1.png" id="Fig1" >}}
Fig. 1. Experimental task procedures and behavioral results of AB task.

**Results**

Our study attempts to optimize BCI performance by enhancing brain signals through cognitive training. Firstly, we successfully replicated the experimental results of Choi et al. by confirming that color-salient training can effectively eliminate AB. Secondly, given that cognitive training affects behavior by altering brain activation and neuronal activity associated with the training task, we explored the underlying neural mechanisms of AB elimination. Our ERP results indicate that color-salient training led to a decrease in the magnitude of T1-elicited P3, which implied a reduction in the allocation of attention to T1 for enhancing T2 detection. This observation can be interpreted as relieving attentional suppression of T2 by preventing over-commitment of attention toward T1, achieved by optimizing the efficient deployment resources. Our ERP findings are also closely paralleled with those of Slagter et al. (2007), who attempted to utilize meditation training to attenuate AB and interpreted their findings as indicative of increased attentional control over the allocation of limited attentional resources. Thus, our results support that the neural mechanism of color-salient training is indeed an attention-based improvement.

Furthermore, our research extended to exploring the impact of color-salient training on RSVP surveillance tasks. The observed improvement in behavioral response accuracy suggests that the training gains can be far transferred to both HTPS and LTPS tasks. However, despite the absence of AB in the LTPS task, trained subjects showed a significant improvement in behavioral performance. This improvement is attributed to the transferability of training gains, indicating enhanced attentional control mechanisms in trained individuals, involving target selection and distractor inhibition. Notably, the AB task entails a dual-target paradigm using digit and letter stimuli, whereas the RSVP surveillance task involves a multi-target setting with image stimuli, which implies that the transferable training gains are not specific to the types or numbers of stimuli. 

In addition, the most noteworthy and encouraging result of this study is that the enhanced brains yield superior RSVP-based BCI performance, regardless of whether an independent or joint training model was employed. We attribute the improvement in BCI performance to two pivotal factors. On the one hand, we have demonstrated that training increases subjects' attentional control, and the similarity between the EEG representations of targets and non-targets neighboring targets diminishes, which enhances the discriminability of EEG representations, thereby significantly reducing the FP. On the other hand, training eliminates AB, which facilitates subjects to see otherwise invisible targets and brains to elicit otherwise lost P3, reducing the FN. Furthermore, we infer that the LTPS task only benefits from the former factor since it does not involve AB, while the HTPS task might benefit from both factors. The fact that both behavioral response accuracy and EEG decoding metrics indicate that the HTPS task benefits more from training than the LTPS task, supports this inference.

**Conclusion**

We have validated the RSVP-based BCI performance achievable by trained users in scenarios with a 20\% target percentage, and where the target stimulus was deliberately set and AB was inevitable. We found that even at this level of difficulty, trained subjects can still reach a considerable performance. We also explored scenarios with a low target percentage that are currently widely used by researchers, and we found that even though state-of-the-art algorithms can decode and classify brain signals accurately, the performance of the BCI system can still be further improved by optimizing the brain signals.

</font>