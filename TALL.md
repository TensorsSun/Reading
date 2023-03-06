# TALL: Temporal Activity Localization via Language Query （ICCV 2017）

## Sumary  
首先提出了视频事件定位的定义，并把视频事件定位表述为"Temporal Activity Localization via Language Query"。阐述了TALL任务面临的两个问题：
* 如何表征text/video特征以进行多模态匹配；
* 如何在有限粒度的SW下准确定位Query。  

主要贡献为：
* 提出了一种新的任务即TALL，并且提供了处理该任务的范式；
* 设计了一种新的跨模态边界回归定位器，联合text/video clip估计对齐分数以及事件的时间边界。

## Method
![1.png](https://s2.loli.net/2023/03/06/aFiYRVtAvxJXoTg.png)
模型框架如上图所示