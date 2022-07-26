---
layout: post
title: 关于在超算的Notebook上装包的记录
categories: Blog
description: none
keywords: 博客
---

在超算的notebook里面装包的话，往往要用到!pip install



然而，在超算使用时需要先调用module load proxy/1.0.0 来开启网络线路



因此，在启动notebook前，要先输入上述代码，以确保网络线路开启



另外直接在termial里面装是不行的，在notebook中仍旧是无法使用。
