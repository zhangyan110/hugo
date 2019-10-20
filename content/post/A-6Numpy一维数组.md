---
author: "张大仙儿"
date: 2019-08-09
title: "认识Numpy库和一维数组"
tags: ["Numpy"]
categories: ["Python数据分析之Numpy"]
---

# 了解Numpy

Numpy是python的一种来源的数值计算扩展。一个重要的特征是它的*数组计算*，是数据分析不可或缺的重要工具包。这个工具可用来存储和处理大型的矩阵，比python自身的嵌套列表结构更加高效。

- 导入Numpy 库需要使用import，后面可自定义简称：

```python
In [1]:import numpy as np
```

- 调用Numpy库中的函数就可用简称np.：

```python
In [2]:np.array()
```

- 也可以把numpy库中的函数导入进来，不过要注意如导入的函数名和python基本函数名相同，就会有冲突报错：

```python
In [3]:from numpy import random  
```

# Numpy的数组对象

我们先来看一组不用Numpy数组的列表操作：

```python
In [4]:a = [1,2,3,4]
       b = [2,3,4,5]
In [5]:[x + 1 for x in a]   #a的各元素都加1
Out[5]:[2, 3, 4, 5]
In [6]:[x + y for (x,y) in zip(a,b)]   #a 和 b的各元素相加，其中zip是打包命令
Out[6]:[3, 5, 7, 9]
```

这样比较繁琐的操作，在有了numpy之后，就简单了很多：

```python
In [7]:a = np.array(a)
       b = np.array(a)
In [8]:a
Out[8]:array([1, 2, 3, 4])
In [9]:b
Out[9]:array([2, 3, 4, 5])
In [10]:a + 1       #a的各元素加1
array([2, 3, 4, 5])
In [11]:a + b      #a 和 b的各元素相加
array([3, 5, 7, 9])
```

## 一维数组的生成方法：

### 1、array方法：

1. 主要形式就是**np.array()**

2. 从列表生成数组：上面的例子就是从列表a，b生成的数组a，b

3. 当然也可以直接将列表传入  np.array([ ])

   ```python
   In [12]:np.array([1,2,'string',[0,5,6]])
   Out[12]:array([1, 2, 'string', list([0, 5, 6])], dtype=object)
   ```

### 2、特定的numpy函数生成特殊数组：

1. 生成全0的数组 **np.zeros()**：

   ```python
   In [13]:np.zeros(5)       #括号里是0的个数
   Out[13]:array([0., 0., 0., 0., 0.])    #默认是float类型,也可以定义类型
   ```

2. 生成全1 数组 **np.ones()**：

   ```python
   In [14]:np.ones(4,dtype = 'int')
   Out[14]:array([1, 1, 1, 1])
   ```

3. 使用 **fill()**方法将数组全部数值设为指定值，需要注意的是：fill()传入的指定值得类型必须与原数组一致：

   ```python
   In [15]:a = np.array([1,2,3,4])
   In [16]:a.fill(5)
   In [17]:a
   Out[17]:array([5, 5, 5, 5])
   In [18]:a = a.astype('float')    #改变数值类型
   In [19]:a.dtype          #查看数组内部数值类型
   Out[19]:dtype('float64')
   In [20]:a.fill(2.5)
   In [21]:a
   Out[21]:array([2.5, 2.5, 2.5, 2.5])
   In [22]:type(a)      #查看a的类型
   Out[22]:numpy.ndarray   #是numpy的数组类型
   ```

4. 生成整数数组 **np.arange()**：

   ```python
   In [23]:a = np.arange(10)   #从0开始到9，左闭右开
   In [24]:a
   Out[24]:array([0, 1, 2, 3, 4, 5, 6, 7, 8, 9])  
   In [25]:np.arange(1,10)   #指定从1到9，同左闭右开
   Out[25]:array([1, 2, 3, 4, 5, 6, 7, 8, 9])
   In [26]:np.arange(1,10,2)   #指定从1到9，每隔2个数取一个
   Out[26]:array([1, 3, 5, 7, 9])
   
   ```

   

5. 生成等差数列 **np.linspace()**：

   ```python
   In [27]:np.linspace(1,100,10)   #从1到100，左闭右闭，包括100，取10个等差的数，默认float
   Out[27]:array([  1.,  12.,  23.,  34.,  45.,  56.,  67.,  78.,  89., 100.])
   ```

6. 生成随机数组 **np.random()**：

   ```python
   In [28]:np.random.rand(10)   #默认取0到1之间的随机数，括号内为个数
   Out[28]:array([0.59597503, 0.18817022, 0.72678016, 0.91498403, 0.76042818,
          0.60486677, 0.07209276, 0.0277797 , 0.73523415, 0.80556396])
   In [29]:np.random.randn(10)  #10个0到1之间的符合标准正态分布的随机数
   Out[29]:array([ 0.08614241, -3.39640225,  0.15740031,  0.7869656 , -0.40755784,
          -1.0842946 ,  1.1977433 ,  1.19857525,  1.23038346,  1.98851508])
   In [30]:np.random.randint(1,10,10)   #1到10之间的10个随机整数
   Out[30]:array([6, 3, 3, 1, 5, 2, 6, 5, 6, 8])
   ```

## 数组属性

- 查看类型：**type**(arr)
- 查看数组中的数值类型：arr.**dtype**
- 更改数组内部数值类型：arr.**astype()**
- 查看形状，会返回一个元组，每个元素代表这一维的元素数目：arr.**shape**

```python
In [31]:arr = np.random.randn(6)
In [32]:arr.shape
Out[32]:(6,)     #表示arr在一维上有6个数值
```

- 数组里面元素的数目：arr.**size**

```python
In [33]:arr.size
Out[33]:6
```

- 查看数组的维度：arr.**ndim**

```python
In [34]:arr.ndim
Out[34]:1
```

## 一维数组索引和切片

- 数组的索引和列表类似：

```python
In [35]:a = np.arange(6)
In [36]:a
Out[36]:array([0, 1, 2, 3, 4, 5])
In [37]:a[0]
Out[37]:0
In [38]:a[0] = 6
In [39]:a
Out[39]:array([6, 1, 2, 3, 4, 5])
In [40]:a[-1]
Out[40]:5
```

- 一维数组的切片，也同样支持负索引：

```python
In [41]:a[1:3]
Out[41]:array([1, 2])
In [42]:a[1:-2]
Out[42]:array([1, 2, 3])
In [43]:a[-4:3]
Out[43]:array([2])
```

- 切片也可以省略参数：

```python
In [44]:a[::2]
Out[44]:array([0, 2, 4])
In [45]:a[1:] - a[:-1]
Out[45]:array([1, 1, 1, 1, 1])
```





