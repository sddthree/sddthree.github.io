---
layout: post
title: 关于在超算中使用tensorboard进行可视化的问题
categories: Blog
description: none
keywords: 博客
---

z在超算使用tensorboard logdirs 时，排除其他影响后发现version `GLIBC_2.18‘ not found的问题。故采用如下方式进行结局。

#### 一、下载包

wget http://ftp.gnu.org/gnu/glibc/glibc-2.18.tar.gz 
#### 二、解压

tar -zxvf glibc-2.18.tar.gz
#### 三、进入目录

cd glibc-2.18
#### 四、创建一个build文件夹，并且进入

mkdir build

cd build/
#### 五、编译安装

../configure --prefix=/usr --disable-profile --enable-add-ons --with-headers=/usr/include --with-binutils=/usr/bin
#### 六、执行(很慢)

make -j 8
#### 七、最后执行

make install

————————————————
链接：https://blog.csdn.net/qq_39648029/article/details/121247564
