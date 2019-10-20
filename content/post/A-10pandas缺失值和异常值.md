---
author: "张大仙儿"
date: 2019-08-19
title: "pandas缺失值和异常值"
tags: ["Pandas -1"]
categories: ["Python数据分析之Pandas"]
---

# 缺失值：

## 判断是否存在缺失值：`df.isnull()`    返回bool值，缺失值都为True

- `df.['列名'].isnull()`：判断某列是否有缺失值,也可以结合`loc[]`进行选择
- `df[df['列名'].isnull()] [:10]` ：判断并列出前十行
- 让我们用之前的例子：

```python
In [1]:df = pd.DataFrame({'A':1.,
      'B':pd.Timestamp('20180101'),
      'C':pd.Series(1,index = list(range(4)),dtype = float),
      'D':np.array([3]*4,dtype = int),
      'E':pd.Categorical(['test','train','test','train']),
      'F':'acb'})
In [2]:df.loc[:2,'D'] = np.nan
In [3]:df['等级'] = ['优','良','中','差']   #插入一列类型不同的吧
In [4]:df
```

​       下面是我截的图：df       

  <img src="https://graph.baidu.com/resource/111541ec1c05b3986984701571038530.jpg"  />

```python
In [5]:df.loc[:,'D'].isnull()
Out[5]:0     True
       1     True
       2     True
       3    False
       Name: D, dtype: bool
In [6]:df[df['D'].isnull()][1:]
Out[6]:      A    B         C    D   E      F  等级
       1	1.0	2018-01-01	1.0	NaN	train	acb	良
       2	1.0	2018-01-01	1.0	NaN	test	acb	中
```

## 处理缺失值：填充 和 删除

- 处理方法一：填充  fillna()
  1. `df.fillna(一个标量)`
  2. `df.fillna(Series, index必须是原DataFrame的需要填充缺失值的columns)`
  3. `df.fillna(dict，keys必须是columns)`
  4. `df.fillna(DataFrame，columns必须是原columns)`

```python
In [7]:s = pd.Series({'A':2.1,'B':pd.Timestamp('20180102'),
                      'C':1.1,
                      'D':9,
                      'E':'test',
                      'F':'aas',
                   '等级':'菜鸟'})  
In [8]:s.name = 4
In [9]:df = df.append(s)     #给df插入一行
In [10]:df
Out[10]:
```

下面是我的截图：df

![](https://graph.baidu.com/resource/111dfd7355e7b88810a9c01571040098.jpg)\

```python
In [11]:df1 = df.copy()
In [12]:df1['D'].fillna(0)       #不会更改df1
Out[12]:0    0.0
        1    0.0
        2    0.0
        3    3.0
        4    9.0
        Name: D, dtype: float64
In [12]:df1['D'] = df1['D'].fillna(0)     #这样就更改了原数据表,或者用参数inplace = True
In [13]:df1
Out[13]:
```

![](https://graph.baidu.com/resource/111aaa01bdf5bbc7ed2e301571040846.jpg) 

```python
In [14]:df3['D'].fillna(np.mean(df3['D']))     #用该列的平均值填充缺失值
Out[14]:0    6.0
        1    6.0
        2    6.0
        3    3.0
        4    9.0
        Name: D, dtype: float64
```

- 处理方法二：删除  dropna()

  1. `df.dropna()` :默认情况下，有缺失值得整行都删除，返回视图
  2. 相关参数有：how = 'all'     当行或者列的元素全为空值的时候，这样的行或列才会被删除

  ​                              inplace = True     覆盖原表数据

  ​                              axis = 0  |    1       选择行或列

```python
In [15]:df.dropna()    #按行，只要有一个空值就会把整行都删掉
Out[15]:
```

![](https://graph.baidu.com/resource/111402ba2546e7dcc82db01571041605.jpg) 

```python
In [16]:df.dropna(axis = 1,inplace = True )      #按列了
In [17]:df
```

![](https://graph.baidu.com/resource/1116dfaa6ea2f451aeb6101571041758.jpg) 

# 异常值（离群点）

- 通过条件选择查找出异常值有哪些

- 对于占比极少数的异常值，可以直接删掉就好
- 也可以利用条件选择，只保留正常值

```python
In [18]:df[df.A > 1.0]   #试图找出异常值 
Out[18]:     A    B          C   D   E       F  等级
       4	2.1	2018-01-02	1.1	9.0	test	aas	菜鸟
In [19]:df = df[df.A < 2.0]   #只保留正常区间的数据
```

