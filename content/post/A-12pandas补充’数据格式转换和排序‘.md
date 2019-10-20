---
author: "张大仙儿"
date: 2019-08-20
title: "pandas补充’数据格式转换和排序‘"
tags: ["Pandas -2"]
categories: ["Python数据分析之Pandas"]
---

# 数据格式转换

- 回归之前的数据格式查看和转换方法：dtype      astype
- 这次用豆瓣电影相关信息的前五名来操作：

```python
In [1]:dd = pd.read_csv(r'C:\Users\dell\Desktop\电影资料.csv')
In [2]:dd
Out[2]:
```

![](https://graph.baidu.com/resource/111a88142a553c3e7181c01571043390.jpg) 

```python
In [3]:dd['投票人数'].dtype
Out[3]:dtype('int64')
In [4]:dd['投票人数'].astype('float')
Out[4]:0    692795.0
       1     42995.0
       2    327885.0
       3    580897.0
       4    478523.0
       Name: 投票人数, dtype: float64
In [5]:
```

- 注意：在进行数据格式转换时如果报错了，可能是因为存在异常值，可以先单独取出来检查一下

# 排序：sort

- 默认排序（根据index) ：`sort_index()`

- 根据某一列进行排序：`sort_values()`

  ```python
  In [5]:dd.sort_values(by = '投票人数')    #默认从小到大，可以ascending = False来从大到小
  Out[5]:
  ```

  ![](https://graph.baidu.com/resource/111e33ce9d9717daf651a01571052589.jpg) 

- 列表也可以同时根据多个指标进行排序

```python
In [6]:dd.sort_values(by = ['评分','投票人数']，ascending = False)
Out[6]:
```

![](https://graph.baidu.com/resource/111c61271eb0acc5b629d01571053032.jpg) 