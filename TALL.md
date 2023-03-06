# TALL: Temporal Activity Localization via Language Query （ICCV 2017）

## Sumary  
首先提出了视频事件定位的定义，并把视频事件定位表述为 ***"Temporal Activity Localization via Language Query"*** 。阐述了TALL任务面临的两个问题：
* 如何表征text/video特征以进行多模态匹配；
* 如何在有限粒度的SW下准确定位Query。  

主要贡献为：
* 提出了一种新的任务即TALL，并且提供了处理该任务的范式；
* 设计了一种新的跨模态边界回归定位器，联合text/video clip估计对齐分数以及事件的时间边界。

## Method
![1.png](https://s2.loli.net/2023/03/06/aFiYRVtAvxJXoTg.png)
模型框架如上图所示，模型分为 **`Visual Encoder`**，**`Sentence Encoder`**，**`Multi Modal Processing`**，**`Temporal Localization Regression Networks`** 四个模块：
* **`Visual Encoder`**
在该模块之前，视频已经使用SW方法被分成了众多帧数相等（不等）的clip，模块同时将每一个clip以及它们的上下文clip作为输入做特征提取，将上下文clip做average pooling。之后将三部分特征连接在一起共同输入进一个线性层就得到了最终的视觉特征。

* **`Sentence Encoder`**
模块尝试了两种句子特征提取方式：LSTM的最后一步隐藏状态；句子编码器 Skip-thought。

* **`Multi-modal Processing Module`**
模块使用三种方式进行模态之间的交互，分别是特征相加，特征相乘以及全连接层输出。将三种方式结合再经过一个全连接层输出即可得到最终的模态交互特征。

* **`Temporal Localization Regression Networks`** 
模块有两个输出：对齐分数以及clip偏移量。本文中作者使用了两种不同的偏移量，“中点-长度”偏移以及“起点-终点”偏移。其中“中点-长度”偏移公式如下所示：
$$ t_c = (p - p_c), t_l = log(l/l_c)$$ 其中，$l$ 和 $p$ 分别代表预测clip的长度以及中心点坐标。

模型的损失函数为：
$$ L = L_{aln} + αL_{reg}$$ $$ L_aln = \frac{1}{N}\sum_{i=0}^N[\alpha log(1 + exp(-cs_{i,i})) + \sum_{j=0,j\neq i}^N\alpha_wlog(1+exp(cs_{i,j}))]$$ $$L_{reg} = \frac{1}{N}\sum_{i=0}^N[R(t_{x,i}^*-t_{x,i})+R(t_{y,i}^*-t_{y,i})]$$其中$R(t)$为smooth $L_1$函数。

采样原则：

## Experiment
本文使用了TACoS和Charades-STA数据集，并且为测试阶段专门生成了更长更复杂的句子。本文在两个数据集上和三个baseline进行了多组对照试验。结果表明模型效果超过了各个baseline模型，且非参数化偏移量比参数化偏移量的效果更好。

## Code




