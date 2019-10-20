---
author: "张大仙儿"
date: 2019-08-16
title: "pandas数据结构"
tags: ["Pandas -1"]
categories: ["Python数据分析之Pandas"]
---

# pandas基本数据结构

pandas内置大量标准库和数据结构，能够有效的处理大型数据集。

使用Pandas需要导入：<u>import  pandas   as   pd</u>

## 1、Series():  本质是一维数组

- Series中能够保存的数据类型也是多样的，但是一个Series中的数据类型必须保持统一。

- Series是有显示的索引，显示在第一列，默认是从0开始，可自定义，定义的索引需保持类型统一。

  ### 一维Series可以用列表初始化：

  ```python
  In [1]:import pandas as pd
         import numpy as np
  In [2]:s = pd.Series([1,3,5,np.nan,6,8])    #np.nan: 是numpy的空值表示
  In [3]:s
  Out[3]:0    1.0
         1    3.0
         2    5.0
         3    NaN
         4    6.0
         5    8.0
         dtype: float64
  ```

  ### Series的一些操作：

  - 查看数据的行标签（索引）：**s.index**

  ```python
  In [4]：s.index          #  查看索引
  Out[4]:RangeIndex(start=0, stop=6, step=1)
  ```

  - 查看值：**values**   和  **切片**

  ```python
  In [5]:s.values
  Out[5]:array([ 1.,  3.,  5., nan,  6.,  8.])   #一维数组
  In [6]:s[0]        #取单个值
  Out[6]:1.0
  In [7]:s[2:5]      #切片取数，默认索引下是左闭右开
  Out[7]:c    5.0
         d    NaN
         e    6.0
         dtype: float64
  In [8]:s[::2]       #间隔两个取值
  Out[8]:a    1.0
         c    5.0
         e    6.0
         dtype: float64
  ```

  - 索引赋值：**name**      索引可以命名，Series本身也可以命名：

  ```python
  In [9]:s.index.name = '索引'
  In [10]:s.name = 'ABC'
  In [11]:s
  Out[11]:
  索引
  a    1.0
  b    3.0
  c    5.0
  d    NaN
  e    6.0
  f    8.0
  Name: ABC, dtype: float64
  In [12]:
  ```

  

## 2、DataFrame：数据框  （二维的）

### 构造方法：

1. 方法一：向DataFrame中**传入数组**：

   首先构造一个时间序列作为第一维的下标；

   然后再创建一个DataFrame结构：

   ```python
   In [12]:date = pd.date_range('20180101',periods = 6)
   In [13]:print(date)
   Out[13]:DatetimeIndex(['2018-01-01', '2018-01-02', '2018-01-03', '2018-01-04',
                  '2018-01-05', '2018-01-06'],
                 dtype='datetime64[ns]', freq='D')
   In [14]:df = pd.DataFrame(np.random.randn(6,4),
                             index = date,columns = list('ABCD'))
   In [15]:df
   Out[15]:          A            B          C           D
       2018-01-01	0.828606	-2.286208	0.228178	-0.879310
       2018-01-02	-0.751154	-0.495647	-1.189315	1.606801
       2018-01-03	-1.645463	-0.818719	1.030602	1.046390
       2018-01-04	-0.142249	-0.680912	-0.281267	0.343966
       2018-01-05	1.475158	-0.259463	-1.696145	0.074144
       2018-01-06	-1.203639	0.925458	-1.849412	-0.566649
   In [16]:
   ```

2. 方法二：**使用字典**传入数据

   字典的每个key代表DataFrame的一列的columns，values就是每列的内容，每列都可以转化为Series，进而DataFrame要求每列的数据类型相同：

   ```python
   In [16]:dt = {'A':1.,
         'B':pd.Timestamp('20180101'),
         'C':pd.Series(1,index = list(range(4)),dtype = float),
         'D':np.array([3]*4,dtype = int),
         'E':pd.Categorical(['test','train','test','train']),
         'F':'acb'}
   In [17]:df2 = pd.DataFrame(dt)
   In [18]:df2
   Out[18]:     A    B          C  D    E      F
            0	1.0	2018-01-01	1.0	3	test	acb
            1	1.0	2018-01-01	1.0	3	train	acb
            2	1.0	2018-01-01	1.0	3	test	acb
            3	1.0	2018-01-01	1.0	3	train	acb
   In [19]:
   ```

### DataFrame的基本操作

- 查看数据：

​     **head()**   :默认查看前五行，可设定行数

​     **tail()**：默认查看后五行，可设定行数

```python
In [20]:df2.head(2)
Out[20]: A    B          C  D    E      F
      0	1.0	2018-01-01	1.0	3	test	acb
      1	1.0	2018-01-01	1.0	3	train	acb
In [21]:df.tail(3)
Out[21]:         A            B           C            D
    2018-01-04	-0.142249	-0.680912	-0.281267	0.343966
    2018-01-05	1.475158	-0.259463	-1.696145	0.074144
    2018-01-06	-1.203639	0.925458	-1.849412	-0.566649
In [22]:
```

- 查看类型： 

  df.**dtypes**  :可查看每个列的类型：

```python
In [22]:df.dtypes
Out[22]:A    float64
        B    float64
        C    float64
        D    float64
        dtype: object
In [23]:
```

-  查看索引和数据：

  df.**index**：行标签

  df.**columns**：列标签

  df.**values**：全部数据     

```python
In [24]:df.index
Out[24]:DatetimeIndex(['2018-01-01', '2018-01-02', '2018-01-03', '2018-01-04',
               '2018-01-05', '2018-01-06'],
              dtype='datetime64[ns]', freq='D')
In [25]:df.columns
Out[25]:Index(['A', 'B', 'C', 'D'], dtype='object')
In [26]:df.values
Out[26]:
array([[ 0.82860603, -2.28620811,  0.22817842, -0.87931012],
       [-0.75115377, -0.49564665, -1.18931516,  1.6068006 ],
       [-1.64546283, -0.8187186 ,  1.03060158,  1.04639038],
       [-0.14224875, -0.68091204, -0.28126694,  0.34396629],
       [ 1.47515817, -0.25946285, -1.6961454 ,  0.07414434],
       [-1.20363919,  0.9254583 , -1.84941209, -0.56664908]])
In [27]:
```

