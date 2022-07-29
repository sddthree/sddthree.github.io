---
layout: post
title: 关于在超算上使用A100的记录
categories: Blog
description: none
keywords: 博客
---

在超算的notebook里面使用torch环境加载A100gpu的话，需要重新装载torch



因为超算原本的cuda是9.0，而torch 版本是1.10适配的是9.0的cuda, 因此要重新装载cuda/11.x, 以及更高版本的torch, 参见[pytorch官方](https://pytorch.org/get-started/locally/)
