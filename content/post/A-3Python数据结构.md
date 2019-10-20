---
author: "张大仙儿"
date: 2019-08-03
title: "数据结构"
tags: ["python基础"]
categories: ["Python数据分析"]
---

# 列表（list）：[ ]

列表中的各个元素可以是各种不同数据类型，也可以是列表本身，或者是字典、集合、元组等。

```python
In [1]:a = [12,'string',[1,2,'张大仙儿']]
```

## 列表操作

- 列表相加 + ：列表之间按照顺序排列

- 元素提取（索引）和切片：

  ```python
  In [2]:a = [1,2,3,'string',['asd',66]]
  In [3]:a[1]
  Out[3]:2
  In [4]:a[4]
  Out[4]:['asd',66]
  In [5]:a[1:4]     #切片，左闭右开
  Out[5]:[2,3,'string']
  In [6]:a[:3]      #默认从0元素开始
  Out[6]:[1,2,3]
  ```

- 向列表中增加元素，有两个方法：

  1. `append()`方法：在列表的末尾增加元素

     ```python
     In [7]:a
     Out[7]:[1,2,3,'string',['asd',66]]
     In [8]:a.append(100)
     In [9]:a
     Out[9]:[1, 2, 3, 'string', ['asd', 66], 100]
     ```

  2. `insert()` 方法：在什么位置插入什么元素

     ```python
     In [10]:a.insert(1,10)
     In [11]:a
     Out[11]:[1, 10, 2, 3, 'string', ['asd', 66], 100]
     ```

- 在列表中删除元素，用pop()方法：

  ```python
  In [12]:a.pop()      #默认删除最后一个元素，并返回
  Out[12]:100
  In [13]:a
  Out[13]:[1, 10, 2, 3, 'string', ['asd', 66]]
  In [14]:a.pop(2)     #删除索引位置为2的元素
  Out[14]:2
  In [15]:a
  Out[15]:[1, 10, 3, 'string', ['asd', 66]]
  ```

- 补充切片的间隔取数：

  ```python
  In [16]:b = [1,2,3,4,5,6,7,8,9,10]
  In [17]:b[2:9:3]   #从第三个元素到第九个元素，每隔三个数取一个
  Out[17]:[3,6,9]
  In [18]:b[9:2:-3]  #从第十个元素到第三位元素（不包括），倒着每隔三个取一个
  Out[18]:[10,7,4]
  ```

- 补充---**列表生成式**：用逻辑语句生成列表

  ```python
  In [43]：list(range(1,11))
  Out[43]:[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
  In [44]:[x**2 for x in range(1,10)]
  Out[44]:[1, 4, 9, 16, 25, 36, 49, 64, 81]
  In [45]:[i for i in range(1,100) if i%10 == 0]
  Out[45]:[10, 20, 30, 40, 50, 60, 70, 80, 90]
  In [46]:[int(x) for x in list('123456')]
  Out[46]:[1, 2, 3, 4, 5, 6]
  ```

  

# 元组 tuple  ()

元组用（）表示，除了初始化后不可以改变外，其余特征和方法都和列表类似。

```python
In [19]:a = (1,'string',(1,2,'a'),[23,45])
In [20]:a[0]
Out[20]:1
In [21]:a[0] = 11    #这是赋值语法，列表也是一样
Out[21]: #报错
```

# 字典 dict  {}

字典用 {key : value} 形式生成，字典内的数据可以是任何数据类型。

- 从字典中取元素：

```python
In [22]:mv = {'names':'肖申克的救赎','actor':'罗宾斯','score':'9.6'}
In [23]:mv['names']
Out[23]:'肖申克的救赎'
In [24]:mv.keys()
Out[24]:dict_keys(['names', 'actor', 'score'])
In [25]:mv.values()
Out[25]:dict_values(['肖申克的救赎', '罗宾斯', '9.6'])
In [26]:mv.items()
Out[26]:dict_items([('names', '肖申克的救赎'), ('actor', '罗宾斯'), ('score', '9.6')])
```

- 修改原有字典内容：

```python
In [27]:mv['names'] = '泰坦尼克号'
In [28]:mv
Out[28]:{'names': '泰坦尼克号', 'actor': '罗宾斯', 'score': '9.6'}
In [29]:mv['director'] = 'zhangdaxian'
In [30]:mv
Out[30]:{'names': '泰坦尼克号', 'actor': '罗宾斯', 'score': '9.6', 'director':               'zhangdaxian'}
In [31]:mv.pop('director')
'zhangdaxian'
In [32]:mv
Out[32]:{'names': '泰坦尼克号', 'actor': '罗宾斯', 'score': '9.6'}
```

# 集合 set  {}

集合也是用{}表示的，最大的特点是：其中的元素没有重复的，生成时可以重复，但它会自动检测是否重复，并保留元素的唯一值。

```python
In [33]:s = {2,3,4,2}
In [34]:s
Out[34]:{2,3,4}
In [35]:len(s)
Out[35]:3
In [36]:s.add(5)
In [37]:s
Out[37]:{2,3,4,5}
In [38]:m = {2,6,5,7}
In [39]:m&s
Out[39]:{2,5}
In [40]:m|s
Out[40]:{2,3,4,5,6,7}
In [41]:s - m
Out[41]:{3,4}
In [42]:m - s
Out[42]:{6,7}
```

