---
author: "张大仙儿"
date: 2019-08-17
title: "pandas数据操作"
tags: ["Pandas -1"]
categories: ["Python数据分析之Pandas"]
---

# Pandas读取数据和数据操作

## 文本格式数据的读写

- 将表格型数据**读取**为DataFrame对象是pandas的重要特性，要实现该功能，基本函数形式：**read_'文本类型‘**

比如：read_csv、read_excel、read_table、read_hdf等。

这些函数的可选参数主要有以下几张类型：

1. *索引*：

   可以将一个或多个列作为返回的DataFrame，从文件或用户处获得列名，或者没有列名。

2. *类型推断和数据转换*：

   包括用户自定义的值转换和自定义的缺失值符号列表

3. *日期时间解析*：

   包括组合功能，也包括将分散在多个列上的日期和时间信息组合成结果中的单个列。

4. *迭代*：

   支持对大型文件的分块迭代

5. *未清洗数据问题*：

   跳过行、页脚、注释以及其他次要数据，比如使用逗号分隔千位的数字。

   

- 在进行表格型数据读取的时候，需要特别注意路径的问题：

  df = pd.read_excel('zhangdaxian.xlsx')   :数据文件和打开的notebook**在**同一路径下

  df = pd.read_excel(r'全路径')   ：数据文件和打开的notebook**不在**同一路径下

  在全路径前面加r是为了避免转义字符\  的问题。

- 将数据**写入**到外部表格文件中：

  

## 数据读取之后的操作

### 行操作:iloc[ ]  和  loc[ ]

- iloc [ ] : 里面是默认的从0开始的索引
- loc [ ]  : 里面是自定义的行标签

```python
In [1]:s = pd.Series(np.arange(4),dtype = int,index = list('abcd'))
In [2]:s
Out[2]:a    0
       b    1
       c    2
       d    3
       dtype: int32
In [3]:s.iloc[0]
Out[3]:0
In [4]:s.iloc[:3]     #左闭右开
Out[4]:a    0
       b    1
       c    2
       dtype: int32
In [5]:s.loc['b']
Out[5]:1
In [6]:s.loc[:'c']     #左闭右闭
Out[6]:a    0
       b    1
       c    2
       dtype: int32
In [7]:
```

### DataFrame后添加一行：df.append(s)

- 在原有表后增加一行，并覆盖原表

```python
In [7]:df = pd.DataFrame({'A':1.,
      'B':pd.Timestamp('20180101'),
      'C':pd.Series(1,index = list(range(4)),dtype = float),
      'D':np.array([3]*4,dtype = int),
      'E':pd.Categorical(['test','train','test','train']),
      'F':'acb'})
In [8]:df
Out[8]:      A    B          C  D    E       F   
       0	1.0	2018-01-01	1.0	3	test	acb
       1	1.0	2018-01-01	1.0	3	train	acb
	   2	1.0	2018-01-01	1.0	3	test	acb
       3	1.0	2018-01-01	1.0	3	train	acb
In [9]:s = pd.Series({'A':2.1,'B':pd.Timestamp('20180102'),
                      'C':1.1,
                      'D':4,
                      'E':'test',
                      'F':'aas'})     
In [10]:s.name = 4    #定义插入的行的索引，以有序插入原数据框
In [11]:df = df.append(s)
In [12]:df
Out[12]:     A    B         C   D    E       F
       0	1.0	2018-01-01	1	3	test	acb
       1	1.0	2018-01-01	1	3	train	acb
       2	1.0	2018-01-01	1	3	test	acb
       3	1.0	2018-01-01	1	3	train	acb
       4	2.1	2018-01-02  1.1 4   test    aas       
    
```

### 删除行：drop([索引])

```python
In [13]:df = df.drop([0])
In [14]:df
Out[14]:     A    B         C   D    E       F
       1	1.0	2018-01-01	1	3	train	acb
       2	1.0	2018-01-01	1	3	test	acb
       3	1.0	2018-01-01	1	3	train	acb
       4	2.1	2018-01-02  1.1 4   test    aas 
```

### 列操作：

- 查看所有列的名称：**df.columns**
- 查看所有行的索引：**df.index**
- 查看某一列的内容：**df['列名']**
- 查看某列前五行内容： **df['列名'] [:5]**
- 查看某两列的前五行的内容： **df[ [ '列 1'，'列 2'] ] [:5]**

```python
In [15]:df.columns
Out[15]:Index(['A', 'B', 'C', 'D', 'E', 'F'], dtype='object')
In [16]:df.index
Out[16]:Int64Index([0,1, 2, 3, 4], dtype='int64')
In [17]:df['C']
Out[17]:0    1.0
        1    1.0
        2    1.0
        3    1.0
        4    1.1
        Name: C, dtype: float64
In [18]:df['B'][:3]
Out[18]:0   2018-01-01
        1   2018-01-01
        2   2018-01-01
        Name: B, dtype: datetime64[ns]
In [19]:df[['A','C']][:3]
Out[19]:     A   C
       0	1.0	1.0
       1	1.0	1.0
       2	1.0	1.0
```

- 增加列：比如说我们给df增加‘*等级*’这一列

```python
In [20]:df['等级'] = ['优','良','中','差','很差']
In [21]:df
Out[21]:     A    B         C   D     E     F  等级
       0	1.0	2018-01-01	1.0	3	test	acb	优
       1	1.0	2018-01-01	1.0	3	train	acb	良
       2	1.0	2018-01-01	1.0	3	test	acb	中
       3	1.0	2018-01-01	1.0	3	train	acb	差
       4	2.1	2018-01-02	1.1	4	test	aas	很差
```

- 删除列：drop()  中指定axis = 1 就可以了

```python
In [22]:df.drop('等级',axis = 1)
Out[22]:     A    B         C   D    E       F
       0	1.0	2018-01-01	1	3	test	acb
       1	1.0	2018-01-01	1	3	train	acb
       2	1.0	2018-01-01	1	3	test	acb
       3	1.0	2018-01-01	1	3	train	acb
       4	2.1	2018-01-02  1.1 4   test    aas
```

- 通过标签选择数据：loc

​       df.loc[1,'列名'] ：选择第一行的第’列名‘ 列的某一个数据

​       df.loc[[1,2,3]，['列 1'，'列 2']]  ：取多个数据

```python:
In [23]:df.loc[1,'B']
Out[23]:Timestamp('2018-01-01 00:00:00')
In [24]:df.loc[[0,2,3],['B','F']
Out[24]:      B          F
       0	2018-01-01	acb
       2	2018-01-01	acb
       3	2018-01-01	acb
```

### 条件选择

```python
In [25]:df['F'] == 'acb'      #返回bool型的Series
Out[25]:0     True
        1     True
        2     True
        3     True
        4    False
        Name: F, dtype: bool
In [26]:df[df['F'] == 'acb'][:3]      #显示出来具体数据
Out[26]:     A    B          C  D    E       F
        0	1.0	2018-01-01	1.0	3	test	acb	
        1	1.0	2018-01-01	1.0	3	train	acb	
        2	1.0	2018-01-01	1.0	3	test	acb	
In [27]:df[(df.A == 1) & (df.E == 'train')][:3]     #两个条件同时满足
Out[27]:     A    B          C  D    E       F
        1	1.0	2018-01-01	1.0	3	train	acb	
        3	1.0	2018-01-01	1.0	3	train	acb	
In [28]:df[((df.A == 1) | (df.A == 2.1)) & (df.F == 'test')]
Out[28]:     A    B         C   D    E       F
       0	1.0	2018-01-01	1.0	3	test	acb	
       2	1.0	2018-01-01	1.0	3	test	acb	
       4	2.1	2018-01-02	1.1	4	test	aas	
```

