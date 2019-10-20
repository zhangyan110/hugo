---
author: "张大仙儿"
date: 2018-09-28
title: "python环境搭建"
tags: ["安装"]
categories: ["Python数据分析"]
---

# 安装与设置

笔者使用的是免费的Anoconda 开发版本，标椎开发环境是Ipython（命令行）和 Juypyter notebook（文本编辑器），区别于功能更为丰富的集成开发环境（IDE）。

## Windows 安装

- 首先官网下载Anaconda安装器 ，版本最新为好

- 下载完成后，检查设置是否正确：打开命令应用（cmd），通过输入python来启动python解释器，可看到相关版本信息。另外，在python解释器中，可以一行一行的执行python脚本，enter键执行，exit（）可退出解释器。Ipython是更具有交互式的python解释器。

- 关于Anaconda有这么几点:

  1、是一个platform : 著名的python数据科学平台

  2、750+流行的python和R数据包，其中有720+是python 的

  3、跨平台的：windows  mac  linux

  4、conda工具：可拓展的包管理工具

  5、免费的

  6、有非常活跃的社区

## 安装及更新Python包

Anaconda下载后自带一些内建包，但也有一些包需要手动进行安装或更新，一般有两种方式：

1. conda 方法：安装：conda   install    *package_name*               更新：conda   update   *package_name*
2. pip      方法：安装：pip  install  *package_name*                        更新：pip install --upgrade   *package_name*

## python包管理工具conda和pip

- 需要注意的是：conda作为一个特殊工具，存在于系统和各种软件及包之间，可在系统之上创建很多新的evironment,并对其进行管理；在evironment中再安装所用packages比如python   pandas等，并对其进行管理。

- 相比于pip，conda更具有扩展性，所以一般用conda进行包安装和更新比较好，而且用conda安装的包不要用pip进行更新，相反也一样。

  （一）、conda的evironment管理：

  1、创建一个新的evironment

  conda create - -name python34 python=3.4

  2、激活一个evironment

     activate python34      #for windows                            

  source activate python34     # for mac / linux

  3、退出一个eviroment

    Deactivate python34      # for windows

    Source deactivate python34      # for mac/linux

  4、删除一个eviroment

    Conda remove - -name python34 - -all

  以上的python34是指eviroment的名字

   

  （二）、conda的package管理

  1. conda的包管理有点类似pip

  2. Conda install numpy   安装numpy

  3. 查看已经安装的python的包有哪些：

  ​     Conda list

  ​     Conda list -n python34   #查看指定环境安装的python包

  4. 删除一个python包

  ​     Conda remove -n python34 numpy

# 