---
layout: post
title: DiRA-Discriminative, Restorative, and Adversarial Learning for Self-supervised Medical Image Analysis
categories: Blog
description: none
keywords: Medical Image Analysis, Contrastive learning, self-supervised
---


---

l论文阅读系列--自监督学习篇

# 1. **DiRA: Discriminative, Restorative, and Adversarial Learning for Self-supervised Medical Image Analysis**

****

一句话摘要: 整合了 Discriminative learning, restorative learning, and adversarial learning



论文之我问:

## 1.1 这个论文的动机是什么

众所周知，计算机视觉中的自监督学习有Discriminative learning, restorative learning, and adversarial learning，这三种都给自监督学习提供了很大的帮助。但是，当下研究忽视了这三者之间的协同效应(1+1+1)。

<center>
    <img src="/images/posts/blog/Paper/1658722167326.jpg" alt="picture not found" style="zoom:70%;" />
    <br>
</center>

## 1.2 这篇论文的研究框架是什么样的

<center>
    <img src="/images/posts/blog/Paper/1658804191064.jpg" alt="picture not found" style="zoom:70%;" />
    <br>
</center>


全新Loss设置:
$$
L = \lambda _ { d i s } * L _ { d i s } + \lambda _ { r e s } * L _ { r e s } + \lambda _ { a d v } * L _ { a d v }
$$


其中:


$$
L _ { \text { dis } } = \ell ( z _ { 1 } , z _ { 2 } )\\
L _ { r e s } = E _ { x } \operatorname { dist } ( x _ { 1 } , x _ { 1 } ^ { \prime } )\\
L _ { a d v } = E _ { x } [ \log D _ { \phi } ( x _ { 1 } ) ] + E _ { x } [ \log ( 1 - D _ { \phi } ( x _ { 1 } ^ { \prime } ) ) ]
$$


具体解释:
$$
\ell ( z _ { 1 } , z _ { 2 } )
$$
表示距离/相似度

## 1.3 这篇论文的实验效果

<center>
    <img src="/images/posts/blog/Paper/1658800610564.jpg" alt="picture not found" style="zoom:70%;" />
    <br>
</center>
2D对比的使用了:

- 对比模型： MoCov2,  Barlow Twins,  SimSiam
- 数据集: ChestXray14
- 模型架构: 2D U-net with ResNet-50
- 超参设置: 
  - 优化器: Adam
  - $L_{res}$: MSE损失
  - $D _ { \phi }$ : four convolutional layers with the kernel size of 3*×*3
  - batch size: 256
- 设备: 4 Nvidia V100 GPUs
- $\lambda_{res},\lambda_{adv},\lambda_{dis}$ : 10, 0.001, 1
- input images: 224×224
- learning rate:  2e-4 and (*β*1*, β*2) = (0*.*5*,* 0*.*999)

3D对比使用了:

- 对比模型：TransVW
- 数据集: 623 chest CT scans in the LUNA
- 模型架构: 3D U-net + classification head
- 超参设置: 
  - 优化器: Adam
  - $L_{res}$: MSE损失
  - $D _ { \phi }$ : four convolutional layers with the kernel size of 3*×*3×3
  - batch size: 256
- 设备: 4 Nvidia V100 GPUs
- $\lambda_{res},\lambda_{adv},\lambda_{dis}$ : 100, 1, 1
- epoch: 200
- learning rate: 1e-3

Tasks:

-  ChestX-ray14, CheXPert [30], SIIM-ACR [1], and NIH Montgomery [31] for 2D models,

-  LUNA, PE-CAD [41], LIDC-IDRI [2], LiTS [5], and BraTS [4] for 3D models

<center>
    <img src="/images/posts/blog/Paper/1658801785576.jpg" alt="picture not found" style="zoom:70%;" />
    <br>
</center>

<center>
    <img src="/images/posts/blog/Paper/1658801908576.jpg" alt="picture not found" style="zoom:70%;" />
    <br>
</center>

## 1.4 代码参考

**https://github.com/JLiangLab/DiRA**.*

# 参考文献

1. [DiRA](https://arxiv.org/abs/2204.10437)

2. [TransVW](https://arxiv.org/abs/2102.10680v1)

3. [MoCov2](https://arxiv.org/abs/2003.04297)

4. [Barlow Twins](https://arxiv.org/abs/2103.03230)

5. [SimSiam](https://arxiv.org/abs/2011.10566)
