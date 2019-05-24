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


