---
title: Faster-RCNN 中概念对比
typora-root-url: ..
---



## Faster-RCNN 中概念对比



### **容易混淆的概念 bbox anchor RoI loc**

 

**BBox**：全称是bounding box，边界框。

- 其中**Ground Truth Bounding Box**是每一张图中人工标注的框的位置。一张图中有几个目标，就有几个框(一般小于10个框)。
- Faster  R-CNN的预测结果也可以叫bounding box，不过一般叫 **Predict Bounding Box**.

 

**Anchor**：锚框 

- 是人为选定的具有一定尺度、比例的框。一个feature  map的锚的数目有上万个（比如 20000）。

 

**RoI**：region of interest，候选框，候选区域。

- Anchor经过了筛选之后就变成了ROI   Anchor相当于瞎猜   ROI是选择了其中一些靠谱的框出来 不过ROI相比于anchor是加上了位置偏移量（RPN的回归结果）的
- Faster R-CNN之前传统的做法是利用selective  search从一张图上大概2000个候选框框。现在利用RPN可以从上万的anchor中找出一定数目更有可能的候选框。在训练RCNN的时候，这个数目是2000，在测试推理阶段，这个数目是300（为了速度）我个人实验发现RPN生成更多的RoI能得到更高的mAP。

 

**Loc** 位置参数

- Ground Truth Bounding      Box 包含两个部分

- - 位置 gt_loc
  - 类别 gt_label

- ROInet 的输出

- - Loc
  - label

 

在RPN阶段，先**穷举生成千上万个anchor**，然后利用**Ground Truth Bounding Boxes**，训练RPN，而后从anchor中找出一定数目的**候选区域（RoIs**）。RoIs在下一阶段用来训练RoIHead，最后生成**Predict Bounding Boxes**。

![1559098234291](/images/1559098234291.png)