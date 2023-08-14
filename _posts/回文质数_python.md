---
layout: post
cid: 41
title: 回文质数 python
slug: 41
date: 2021/06/01 20:02:49
updated: 2021/06/01 20:07:18
status: publish
author: mi0e
categories: 
  - 编程
  - Python
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


![6-01-2.png][1]


  [1]: http://mioe.xyz/usr/uploads/2021/06/1304133883.png

洛谷卡了很长时间，最终还是没有AC，最后两个超时，可能是我回文判断选择用字符串的方式导致的,最后没办法了，选择下策直接打表AC。

注：

 1. 除 11 外没有偶数位的回文质数，那么[10000000,100000000] 这个区间根本不用枚举。
 2. 只需要[2, sqrt(i) + 1]

代码如下：
```python
    import math
    a, b = map(int, input().split())
    list1 = []
    if b > 10000000:
        b = 10000000
    for i in range(a, b + 1):
        if str(i) == str(i)[::-1]:
            for j in range(2, int(math.sqrt(i)) + 1):
                if i % j == 0:
                    break
            else:
                print(i)
```