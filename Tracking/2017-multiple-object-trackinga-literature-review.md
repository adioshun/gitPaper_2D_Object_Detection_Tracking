[Multiple Object Tracking: A Literature Review](https://arxiv.org/abs/1409.7618)
코드 : https://github.com/YeongjinOh/RapidCheck


여러 제안 들이 있지만 문제점은 존재 한다. `Although different kinds of approaches have been proposed to tackle this problem, it still remains challenging due to factors like`
- abrupt appearance changes and 
- severe object occlusions. 

본 연구에서는 위 문제들에 대한 리뷰를 하겠다. `In this work, we contribute the first comprehensive and most recent review on this problem. `

기여도는 아래와 같다. `The main contributions of this review are fourfold: `
- 1) Key aspects in a multiple object tracking system, including formulation, categorization, key principles, evaluation of an MOT are discussed. 
- 2) Instead of enumerating individual works, we discuss existing approaches according to various aspects, in each of which methods are divided into different groups and each group is discussed in detail for the principles, advances
and drawbacks. 
- 3) We examine experiments of existing publications and summarize results on popular datasets to provide quantitative comparisons. We also point to some interesting discoveries by analyzing these results. 
- 4) We provide a discussion about issues of MOT research, as well as some interesting directions which could possibly become potential research effort in the future.

## 1. INTRODUCTION

MOT는 컴퓨터 비젼에서 중요한 역할을 담당한다. 추적 대상은 사람 부터 차량까지 다양하다. `Multiple Object Tracking (MOT), or Multiple Target Tracking (MTT), plays an important role in computer vision. The task of MOT is largely partitioned to locating multiple objects, maintaining their identities, and yielding their individual trajectories given an input video. Objects to track can be, for example, pedestrians on the street [1], [2],vehicles in the road [3], [4], sport players on the court [5], [6], [7], or groups of animals (birds [8], bats [9], ants [10], fish [11], [12], [13], cells [14], [15], etc.). `


멀티 오브젝트는 어떻게 보면 싱글 오브젝트로도 볼수 있다. `Multiple “objects” could also be viewed as different parts of a single object [16]. `

본 논문에서 추적 대상은 **사람**으로 잡았다. 이유는 다음과 같다. `In this review, we mainly focus on the research on pedestrian tracking. The underlying reasons for this specification are threefold. `
- 사람은 강체가 아니라 좋은 연구 대상이다. `First, compared to other common objects in our environment, pedestrians are typical nonrigid objects, which is an ideal example to study the MOT problem. `
- 사람 추적은 응용 서비스가 많다. `Second, videos of pedestrians arise in a huge number of practical applications, which further results in great commercial potential. `
- 대부분의 연구는 사람 추적에 대해 이루어 진다. `Third, according to all data collected for this review, at least 70% of current MOT research efforts are devoted to pedestrians.`

MOT는 다음 high-level task로 나누어(??grounds) 볼수 있다. `As a mid-level task in computer vision, multiple object tracking grounds high-level tasks such as `
- pose estimation [17], 
- action recognition [18], 
- and behavior analysis [19]. 

여러 응용 서비스 들도 많다. `It has numerous practical applications, such as visual surveillance [20], human computer interaction [21] and virtual reality [22]. These practical requirements have sparked enormous interest in this topic.`

SOT & MOT목적 
- SOT
    - sophisticated appearance models and/or motion models 설계 
    - scale changes, outof-plane rotations and illumination variations 문제 해결 
- MOT 
    - 위 문제 외 추가 2가지 
    - 시간 마다 변하는 물체 **수**
    - 물체 ID 

```
Compared with Single Object Tracking (SOT), which primarily focuses on designing sophisticated appearance models and/or motion models to deal with challenging factors such as scale changes, outof-plane rotations and illumination variations, multiple object tracking additionally requires two tasks to be solved:
- determining the number of objects, which typically varies over time, and 
- maintaining their identities. 
```

MOT에서 주요 이슈는 `Apart from the common challenges in both SOT and MOT, further key issues that complicate MOT include among others:`
- 1) frequent occlusions, 
- 2) initialization and termination of tracks, 
- 3) similar appearance, and 
- 4) interactions among multiple objects. 

여러 연구가 진행 되었지만 다양한 복잡성으로 새연구원들이 접근하기 어렵다. `In order to deal with all these issues, a wide range of solutions have been proposed in the past decades. These solutions concentrate on different aspects of an MOT system, making it difficult for MOT researchers, especially newcomers, to gain a comprehensive understanding of this problem. `

그래서 본 논문을 작성 하였다. `Therefore, in this work we provide a review to discuss the various aspects of the multiple object tracking problem.`

### 1.1 Differences from Other Related Reviews

기존의 여러 리뷰 논문을 분류 하면 아래와 같다. `To the best of our knowledge, there has not been any comprehensive literature review on the topic of multiple object tracking. However, there have been some other reviews related to multiple object tracking, which are listed in Table 1. We group these surveys into three sets and highlight the differences from ours as follows.`

![](https://i.imgur.com/JszNpgL.png)

리뷰논문들의 첫 분류 : The **first set** [19], [20], [21], [23], [24] discusses tracking as an individual part while this work specifically discusses various aspects of MOT. For example, object tracking is discussed as a step in the procedure of high-level tasks such as crowd modeling [19], [23], [24]. Similarly, in [21] and [20], object tracking is reviewed as a part of a system for behavior recognition [21] or video surveillance [20].


리뷰논문들의 두번째 분류 :The **second set** [25], [26], [27], [28] is dedicated to general visual tracking techniques [25], [26], [27] or some special issues such as appearance models in visual tracking [28]. Their reviewing scope is wider than ours; ours on the contrary is more comprehensive and focused on multiple object tracking.


리뷰논문들의 세번째 분류 :The **third set** [29], [30] introduces and discusses benchmarks on general visual tracking [29] and on specific multiple object tracking [30]. Their attention is laid on experimental studies rather than literature reviews.



### 1.2 Contributions

본 논문의 기여와 구성 요소는 아래와 같다. `We provide the first comprehensive review on the MOT problem to the computer vision community, which we believe is helpful to understand this problem, its main challenges, pitfalls, and the state of the art. The main contributions of this review are summarized as follows:`

- 2.1절에서는 문제점을 정의 하고 2.2절에서는 기술 분류 하였다.  `We derive a unified formulation of the MOT problem which consolidates most of the existing MOT methods (Section 2.1), and two different ways to categorize MOT methods (Section 2.2).`

- 3장에서는 구성요소에 대하여 기술 하였다.`We investigate different key components involved in an MOT system, each of which is further divided into different aspects and discussed in detail regarding its principles, advances, and drawbacks (Section 3).`

- 4장에서는 실험 결과와 데이터셋을 기술 하였다. `Experimental results on popular datasets regarding different approaches are presented, which makes future experimental comparison convenient. By investigating the provided results, some interesting observations and findings are revealed (Section 4).`

- 5장에서는 미해결 문제와 연구 방향을 기술 하였다. `By summarizing the MOT review, we unveil existing issues of MOT research. Furthermore, open problems are discussed to identify potential future research directions (Section 5).`


최근 연구 물들을 중심으로 하였다. `Note that this work is mainly dedicated to reviewing recent literature on the advances in multiple object tracking. As mentioned above, we also present experimental results on publicly available datasets excepted from existing publications to provide a quantitative view on the state-of-the-art MOT methods. `

활용된 벤치마킹 [30]이다. `For standardized benchmarking of multiple object tracking we kindly refer the readers to the recent work MOTChallenge by Leal-Taixe´ et al. [30].`


### 1.3 Organization of This Review



### 1.4 Denotations



## 2 MOT PROBLEM

MOT의 문제점을 수학적으로 기술 하였다. We first endeavor to give a general mathematical formulation of MOT. We then discuss its possible categorizations based on different aspects.`

### 2.1 Problem Formulation


### 2.2 MOT Categorization

다음 3가지 criteria에 따라서 분류 하였다. `It is difficult to classify one particular MOT method into a distinct category by a universal criterion. Admitting this, it is thus feasible to group MOT methods by multiple criteria. In the following we attempt to conduct this according to three criteria:`
- a) initialization method, 
- b) processing mode, and
- c) type of output. 

위 3가지를 선택한 이유는 process를 설명하기 직관적이기 때문이다. `The reason we choose these three criteria is that this naturally follows the way of processing a task, i.e., `
- how the task is initialized, 
- how it is processed and 
- what type of result is obtained. 

In the following, each of the criteria along with its corresponding categorization is represented.


#### 2.2.1 Initialization Method

물체가 초기화 되는 방식에 따라 나눌수 있다. `Most existing MOT works can be grouped into two sets [49], depending on how objects are initialized: `
- Detection-Based Tracking (DBT) and 
- Detection-Free Tracking (DFT).

![](https://i.imgur.com/0XXPHuV.png)

##### Detection-Based Tracking

이 방식은 먼저 탐지를 하고 궤도에 연결하는 방식이다. `As shown in Figure 1 (top), objects are first detected and then linked into trajectories.`

**tracking-by-detection**라고도 불리운다. `This strategy is also commonly referred to as “tracking-by-detection”. `

흐름은 `Given a sequence, `
- 각 프레임마다 후보군에 대한 물체 탐지 또는 모션 탐지가 수행 된다. `type-specific object detection or motion detection (based on background modeling) [50],[51] is applied in each frame to obtain object hypotheses, `
- 이후 탐지 후보를 궤도에 연결하는 추적 작업이 수행 된다. `then (sequential or batch) tracking is conducted to link detection hypotheses into trajectories. `

두가지 이슈가 있다. `There are two issues worth noting.`
- 탐지기 학습이 선행 되기에 학습 대상에 의존적이다. `First, since the object detector is trained in advance, the majority of DBT focuses on specific kinds of targets, such as pedestrians, vehicles or faces. `
- 탐지기 성능에 의존성이 크다. `Second, the performance of DBT highly depends on the performance of the employed object detector.`

##### Detection-Free Tracking. 

직접 물체의 수를 지정 해야 한다. 이후프레임에서 해당 물체의 위치를 localized 해준다. `As shown in Figure 1 (bottom), DFT [52], [53], [54], [55] requires manual initialization of a fixed number of objects in the first frame, then localizes these objects in subsequent frames.`


DBT방식 많이 사용된다. DFT는 학습이 불필요한 장점이 있다. `DBT is more popular because new objects are discovered and disappearing objects are terminated automatically. DFT cannot deal with the case that objects appear. However, it is free of pre-trained object detectors.`

Table 3 lists the major differences between DBT and DFT.

![](https://i.imgur.com/R6WV5DN.png)

#### 2.2.2 Processing Mode



