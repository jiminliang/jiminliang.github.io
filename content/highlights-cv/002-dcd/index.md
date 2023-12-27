---
title: Intelligent diagnosis of DCD
date: 2023-12-27
image:
  focal_point: 'top'
---

We developed digital visual-motor systems and algorithms to autonomously evaluate developmental coordination disorder (DCD) and delve into associated pathologies.

<!--more-->

<font size=3>

- **Introduction**

DCD, also referred to as developmental dyspraxia, is a type of neuromotor disorder that affects approximately 5%-6% of school-age children. Children with DCD typically exhibit ‘clumsy’ movements and have limited flexibility in their limbs when participating in some daily activities, such as, playing sports, catching objects, and using scissors. The motor coordination abilities of children with DCD lag far behind that of their peers at typical developmental stages. What’s more, some children with DCD have problems with perceptual, sensory, tactile, and visual perception. Without timely diagnosis and interventions, the symptoms of most children with DCD will continue into adolescence or adulthood, which seriously affects the social, academic, and emotional development of patients, and brings some secondary health problems, such as obesity , depression , and poor social adaptability. Timely assessment is of great importance to the physical and mental health for children with DCD. At present, the etiology and pathogenesis of DCD are unclear.

In our previous works, a marker-less visual-motor tracking system was developed, which captures both eye movement and body motion of children as well as scene information during DCD fine and gross motor assessment. With the help of the designed system, we conducted several studies on fine movements of DCD in the early stage. The automated fine motor evaluation of DCD was achieved by the designed task localization algorithm and task evaluation algorithm (Ruimin Li et. al., TNSRE 2019). 

In this study, we focus on **_developing a framework for behavior analysis in gross movements and mining quantified behavioral markers of children with DCD in the gross tasks_**. Taking the task of throwing beanbag specified in the DCD assessment tool as an example, we investigate the behavior pattern of children with DCD through the analysis of eye movement, body movement, and interacting object trajectory.

- **Behavior Analysis With Integrated Visual-Motor Tracking for Developmental Coordination Disorder**

DCD is a motor learning disability with a prevalence of 5%-6% in school-aged children, which may seriously affect the physical and mental health of affected children. Behavior analysis of children helps explore the mechanism of DCD and develop better diagnosis protocols. In this study, we investigate the behavioral pattern of children with DCD in the gross movement using a visual-motor tracking system. First, visual components of interest are detected and extracted using a series of intelligent algorithms. Then, the kinematic features are defined and calculated to describe the children behavior, including eye movement, body movement, and interacting object trajectory. Finally, statistical analysis is conducted both between groups with different motor coordination abilities and between groups with different task outcomes. The experimental results show that groups of children with different coordination abilities differ significantly both in the duration of eye gaze focusing on the target and in the degree of concentration during aiming, which can serve as behavioral markers to distinguish children with DCD. This finding also provides precise guidance for the interventions for children with DCD. In addition to increasing the amount of time spent on concentrating, we should focus on improving children’s attention levels.

The advanced observation and planning of eyes are crucial in the throwing task. Effective Aiming Time (EAT) reflects the percentage of time that the participants’ eyes effectively focusing on the target mat before the beanbag releasing from the hand. ANOVA test reveals there is a significant group difference on the EAT in Phase 1 (p<0.05, effect size= 0.40, power=0.7833). It is obvious that the group of children with higher motor coordination score spends more time effectively aiming at the target. Relative Gaze Stability (RGS) reflects the stability of the eye gaze points and the degree of concentration during aiming. ANOVA test reveals a significant group difference on the RGS in Phase 1(p<0.005, effect size=0.48, power=0.9153). This kind of high-attention observation in Phase 1 is very like to plan and prepare for the action of throwing the beanbag, which may benefit to an accurate hit. In addition to the quantitative analysis, we also make some
visual analysis below in order to show the group difference intuitively.

{{< figure src="Result_2023_TNSRE.png" >}}

Relative gaze heatmaps of nine samples from the LMC, MMC, and HMC groups. The heatmaps of the samples in the LMC group are the most scattered, and their spread is widest, almost covering the entire red magnified box. Heatmaps of the samples in the MMC group is slightly more concentrated than that of the LMC group, and their spread area only occupies a certain part of the red magnified box. Heatmaps of the samples in the HMC group are the most compact, and they are all concentrated around the target mat.

Read our paper for more details:

Ruimin Li, Hong Fu*, Yang Zheng, Shuiping Gou*, Jane Jie Yu, Xiaowei Kong, Hongmin Wang,  [Behavior Analysis with Integrated Visual-Motor Tracking for Developmental Coordination Disorder](https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=10108003), IEEE Transactions on Neural Systems and Rehabilitation Engineering, 31: 2164-2173, 2023.

</font>