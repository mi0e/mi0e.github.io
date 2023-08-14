---
layout: post
cid: 31
title: 分而治之(D&amp;C）
slug: 31
date: 2021/03/31 18:15:00
updated: 2021/03/31 18:20:28
status: publish
author: mi0e
categories: 
  - 算法
tags: 
customSummary: 
noThumbInfoStyle: default
outdatedNotice: no
reprint: standard
thumb: 
thumbChoice: default
thumbDesc: 
thumbSmall: 
thumbStyle: default
---


**分而治之(Ｄ＆Ｃ)** 能将问题逐步分解，但并非可用于解决问题的算法，而是一种解决问题的思路。

**分而治之算法**是递归的，使用分而治之(D&C)解决问题的过程包括两个步骤：

 1. 找出递归边界条件，这种条件必须尽可能简单
 2. 不断地将问题分解（或者说缩小规模），直到符合递归边界条件。

> **注意**：假设要将一块地均匀地分成方块，确保分出的方块最大的条件，应采取Ｄ＆Ｃ策略：适用于这小块地的最大方块，也是适用于整块地的最大方案。原因可参考欧几里得算法。


----------
给定一个数字数组　arr = [2, 4, 6]，如何将这些数字相加

 1. 找出递归边界条件：数组不包含任何元素或只包含一个元素
 2. 每次递归调用都必须离空数组更近一步。

**例如：**
```python
    arr = [2, 4, 6]
    sum(arr) = 12
    
    #等效于下面的语句
    arr = [4, 6]
    2 + sum(arr) = 12
    
    #再等效下面的语句
    arr = [6]
    2 + 6 + sum(arr) = 12
    
    #依次类推，逐渐缩小了问题的规模
```

> 注意：编写涉及数组的递归函数时，递归边界条件通常是数组为空或只包含一个元素。陷入困境时，请检查递归边界条件是不是这样的。

