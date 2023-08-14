---
layout: post
cid: 61
title: C++ STL容器（11个）
slug: 61
date: 2021/10/23 16:33:00
updated: 2023/02/04 20:04:04
status: publish
author: mi0e
categories: 
  - 编程
  - C/C++
tags: 
customSummary: 
mathjax: auto
noThumbInfoEmoji: 
noThumbInfoStyle: default
outdatedNotice: no
parseWay: auto
reprint: standard
thumb: 
thumbChoice: default
thumbDesc: 
thumbSmall: 
thumbStyle: default
---


# `deque` :

# `list` :

# `queue` :

![](https://mioe-xyz.oss-cn-shanghai.aliyuncs.com/usr/uploads/2022/11/3285107056.jpg)

# `priority_queue` :

#### #### 默认大顶堆（后两参数可缺省）

```
priority_queue<int> big_heap;
```

#### 大顶堆

```
priority_queue<int,vector<int>,less<int>> big_heap2;
```

#### 小顶堆

```
priority_queue<int,vector<int>,greater<int>> small_heap;
```

#### 函数

`bool empty() const`：返回值为true，说明队列为空

`int size() const`：返回优先队列中元素的数量

`void pop()`：删除队列顶部的元素，也即根节点

`int top()`：返回队列中的顶部元素，但不删除该元素

`void push(int arg)`：将元素arg插入到队列之中；

# `stack` :

# `vector` :

# `map` :

# `multimap` :

# `set` :

# `multiset` :

# `bitset` :
