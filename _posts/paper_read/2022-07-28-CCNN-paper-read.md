---
layout: post
title: Towards a General Purpose CNN for Long Range Dependencies in ND
categories: [Paper Read]
description: none
keywords: Medical Image Analysis, Contrastive learning, self-supervised
---

论文阅读系列--CNN网络架构篇

# 1. ****Towards a General Purpose CNN for Long Range Dependencies in** N**D****

****

一句话摘要: 使用小网络来生成kernel实现连续的卷积神经网络每层的Long range dependency



论文之我问:

## 1.1 这个论文的动机是什么

众所周知，计算机视觉中的具有良好性能的CNN架构都需要针对特定任务进行定制，比方说要考虑输入长度啊，分辨率以及输入维度等等。该论文目的是克服这个基于问题定制化的CNN架构。


## 1.2 这篇论文的研究框架是什么样的

<center>
    <img src="/images/posts/blog/Paper/1658980563627.jpg" alt="picture not found" style="zoom:70%;" />
    <br>
</center>

如图1所示。 (a) 表示一个小神经网络$G_{Kernel}$，它的输入是 $corrd_{i}$ , 然后它的输出是在位置K处的卷积核



简而言之，这就是个它可以理解为一个卷积核生成网络

<center>
    <img src="/images/posts/blog/Paper/1658988741457.jpg" alt="picture not found" style="zoom:70%;" />
    <br>
</center>

如图2所示。Continues CNN 架构。

1. 架构的形成: Res block + Position normalization layers + FlexNet ~ S4 networks

2. 深度可分离连续核卷积：分离卷积可以提升计算效率，并可以优化卷积，通过对spatial和channel的分离，先少了计算复杂度和参数复杂度。
3. 核生成网络的初始化：初始化时，为避免出现梯度爆炸或者梯度消失，通常会让卷积层的输入方差等于输出方差。为避免上述情况，在核生成网络的最后一层，重新加权: $gain/\sqrt{in\_channels\cdot kernel\_size}$

## 1.3 这篇论文的实验效果

<center>
    <img src="/images/posts/blog/Paper/1658989206591.jpg" alt="picture not found" style="zoom:70%;" />
    <br>
</center>

CCNN在多种任务上都表现良好，并在一些任务上达到了SOTA


## 1.4 代码参考

**[https://github.com/david-knigge/ccnn](https://github.com/david-knigge/ccnn)**.*

# 参考文献

1. [FlexConv](https://openreview.net/forum?id=3jooF27-0Wy)
2. [CKCNNs]([CKConv: Continuous Kernel Convolution For Sequential Data | OpenReview](https://openreview.net/forum?id=8FhxBtXSl0))
3. [S4networks]([Efficiently Modeling Long Sequences with Structured State Spaces | OpenReview](https://openreview.net/forum?id=uYLFoz1vlAC))
4. [initialization]([Principled Weight Initialization for Hypernetworks | OpenReview](https://openreview.net/forum?id=H1lma24tPB))
