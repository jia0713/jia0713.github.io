---
layout: article
title: MobileNet v1总结
mathjax: true
tags: 机器学习
---

## MobileNet V1

MobileNet是谷歌开发的专注于移动端和嵌入式开发的轻量级CNN网络，MobileNet v1（[论文链接](https://arxiv.org/pdf/1704.04861.pdf)）于2017年发表。MobileNet的最大贡献是提出了深度可分离卷积（depthwise separable convolution）的概念。

## 深度可分离卷积

深度可分离卷积，是由depthwise和pointwise两个部分结合起来，用于提取特征，能够有效的降低参数数量和运算成本。以下说明和图片引用了[这篇博客](https://zhuanlan.zhihu.com/p/92134485)。

### 常规卷积运算

![Normal Convolution](/assets/images/posts/MobileNetConvImage.jpg)

对于一张5×5像素、三通道（shape为5×5×3），经过3×3卷积核的卷积层（假设输出通道数为4，则卷积核shape为3×3×3×4，最终输出4个Feature Map，如果有same padding则尺寸与输入层相同（5×5），如果没有则为尺寸变为3×3. 

### 深度可分离卷积

#### 逐通道卷积（Depthwise Convolution）

Depthwise Convolution的一个卷积核负责一个通道，一个通道只被一个卷积核卷积。

一张5×5像素、三通道彩色输入图片（shape为5×5×3），Depthwise Convolution首先经过第一次卷积运算，DW完全是在二维平面内进行。卷积核的数量与上一层的通道数相同（通道和卷积核一一对应）。所以一个三通道的图像经过运算后生成了3个Feature map(如果有same padding则尺寸与输入层相同为5×5)，如下图所示。

![DepthWise Convolution](/assets/images/posts/depthwiseconv.jpg)

#### 逐点卷积（Pointwise Convolution）

Pointwise Convolution可以理解为kernel size为1的常规卷积。经过Depthwise Convolution运算后的特征图数量和输入图数量是一致的，如果要扩展feature map,就要增加目标chanel数的逐点卷积，有几个卷积核就有几个输出通道数，如下图所示。

![PointWise Convolution](/assets/images/posts/pointwiseconv.jpg)

可以看到经过 Normal Convolution 对比经过 Depthwise Convolution + Pointwise Convolution操作得到的输出在尺度上是完全一致的。

让我们用上面的维度计算以下参数量和乘加计算运算量。

常规卷积，参数量

3 × 3 × 3 × 4 = 108

乘加计算量

（3 × 3 × 3 × 3 + 3 × 3）× 3 × 4 = 1080 次

逐通道卷积，参数量

3 × 3 × 3 = 27

乘加计算量

（3 × 3 × 3 × 3 + 3 × 3）× 3 = 270 次

逐点卷积，参数量

3 × 1 × 1 × 4 = 12

乘加计算量

（3 × 3 + 1）× 3 × 4 = 120

可以看到，用逐通道加上逐点卷积的方式有效的减少了常规卷积的参数量。

## 网络结构

MobileNet v1原文的网络结构如下

![MobileNet v1](/assets/images/posts/mobilenetv1.png)

该网络有28层，值得注意的是，网络用大量的stride代替pooling进行降维。
