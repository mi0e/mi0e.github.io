---
layout: post
cid: 39
title: 洛谷 P1106 删数问题 python解法
slug: 39
date: 2021/06/01 19:48:00
updated: 2021/06/01 20:07:21
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


![6-01-1.png][1]


  [1]: http://mioe.xyz/usr/uploads/2021/06/3479330492.png

第一次提交时，因为读题不清，3个WA。一开始理解为依次删除最大数，例50074897 2得500747，结果一直WA，然后被迫下载测试数据，发现正确答案为 4897。

思索了一番，发现是个贪心问题,还是用 50074897 2 举例:
        (1) 5 > 0 , 删除5, 0074897
        (2) 0 = 0 , 不动 0074897
        (3) 0 = 0 , 同理 0074897
        (5) 7 > 4 , 删除7，004897
        (6) 去零整理，答案为 4897
Python天下第一，代码如下：
```python
    m = input()
    n = int(input())
    i = 0   # 用于下标索引
    while quit:
        # 边界默认和0比
        if i + 1 == len(m):
            m = m[:len(m) - 1]
            n -= 1
            i -= 1
        # 判断是否单调递增
        elif m[i] <= m[i + 1]:
            i += 1
            continue
        # 删除非递增项
        else:
            m = m.replace(m[i], "", 1)
            n -= 1
            i -= 1
        # 循环结束
        if n == 0:
            break
    print(int(m))
```

