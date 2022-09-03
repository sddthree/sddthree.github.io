---
layout: post
title: 关于使用自己数据跑模型时损失函数无法有效下降与cindex无法有效提升的问题
categories: Blog
description: none
keywords: 博客

---

关于使用自己数据跑模型时损失函数无法有效下降与cindex无法有效提升的问题的一些猜想与解决方案

### 1. 模型结构问题

​	可能性较小

​	方案一: 使用经典模型结构进行尝试

​    方案二: 使用预训练的方式构建特征提取过程

​    方案三: 自己构建的模型可以先通过公开数据集进行验证，以确保有效性

### 2. 输入数据预处理问题

 	resize 到 相同范围 -- 改为patch level 的输入

​	单一序列进行测试

### 3. 损失函数问题

​	改为 [EDL](https://papers.nips.cc/paper/2018/hash/a981f2b708044d6fb4a71a1463242520-Abstract.html)([MICCAL 2022](https://www.bilibili.com/video/BV1xT411L7Q1)一篇文章有使用) + 另一loss([Cancer Cell](https://doi.org/10.1016/j.ccell.2022.07.004))

### 4. 多中心异质性问题

​    排除掉异质性大的
