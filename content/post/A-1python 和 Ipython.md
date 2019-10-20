---
author: "张大仙儿"
date: 2019-07-03
title: "python 和 Ipython"
tags: ["认识python"]
categories: ["Python数据分析"]
---

# Python解释器

python是一种解释性的语言，区分于C和JAVA等编译性的语言，python解释器通过一次执行一条语句来运行程序。标准的交互式python解释器可以通过在命令行（cmd）输入python命令来启动。

```python
$ python
>>> a = 5
>>> print(a)
5
```

- 通过python命令，再把.py文件（文件名或文件的全路径）作为第一个参数就可以运行.py文件中的代码。加入我们写了一个叫 art-1.py 的文件，内容是：print('hello world!')

  可以在解释器中运行以下命令来运行程序：（art-1.py 必须在命令行的当前路径下）

  ```python
  $ python art-1.py           #注意这里不是在>>>提示符后的写的
  hello world!
  ```

- 退出python解释器：通过exit()

# Ipython基础

Ipython是一个加强版的python解释器，Juypyter notebook 是一种基于Web的代码笔记本，最初也源于Ipython项目。

## 运行Ipython命令行

可以像启动标椎python解释器那样，通过在命令行（cmd）中输入ipython来启动ipython命令行：

```python
$ ipython
In [1]:a = 5                #In[]:是ipython提示符的形式
In [2]:a
Out[2]:5
```

使用 **%run** 命令时，Ipython会在同一个进程内执行指定文件中的代码，确保你在执行完成后可以立即探索结果。

```python
In [1]: %run art-1.py       #与python不同，是在In[]:提示符后%run 的
hello world!
In [2]:
```

当你在ipython中仅输入一个人变量名，它会返回一个表示该对象的字符串，且是在控制台中打印出：

```python
In [2]:import numpy as np
In [3]:data = {i:np.random.randn() for i in range(7)}
In [4]:data
Out[4]:
    {0:-0.2047                #这是在控制台中打印出来的data的值，相比python的print（）更美观
     1:0.4790
     2:-0.5194
     3:-0.5557
     4:1.9658
     5:0.3934
     6:0.0929}
In [5]:
```

## 运行Jupyter notebook

jupyter项目中的主要组件就是notebook,这是一种交互式的文档类型，可用于编写代码、文本（可以带标记）、数据可视化以及其他输出。Jupyter与内核交互，内核是编程语言的交互式计算协议的实现，python 使用ipython作为内核从而使用jupyter.

### jupyter打开方式：

1. 在终端中运行Jupyter notebook 命令：

   ```python
   $ jupyter notebook
   ```

   在很多平台上，jupyter会自动打开你的默认浏览器，我用的谷歌

2. 通过Anaconda Navigator的客户端平台打开jupyter notebook:

   ![如图](https://graph.baidu.com/resource/111cc6ee739256d52ba8901570781351.jpg)

3. 通过http地址来浏览notebook:  http://localhost:8888/

## Jupyter notebook 的基本使用

### 常用操作

1. 通过新建，选择python3来打开一个新的笔记本

2. Shift + Enter: 执行代码并且移动光标到下一行

3. Ctrl  + Enter :执行并且光标不会移动至新的一行

4. d d :删除多余cell

5. 添加标题单元格时，选择‘标题（headings）‘类型：

   “#” ：一级标题         

   “##” ：二级标题    （中间无空格，但与标题之间有空格）

   以此类推

6. 正常输入代码，都是在“代码（code）”类型下

7. 做注释，就选择“标记（marknote）”类型

### 