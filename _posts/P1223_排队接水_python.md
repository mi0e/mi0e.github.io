---
layout: post
cid: 42
title: P1223 排队接水 python
slug: 42
date: 2021/06/02 21:10:00
updated: 2021/06/02 21:23:20
status: publish
author: mi0e
categories: 
  - 编程
  - Python
  - 算法
tags: 
customSummary: 
mathjax: auto
noThumbInfoStyle: default
outdatedNotice: no
reprint: standard
thumb: 
thumbChoice: default
thumbDesc: 
thumbSmall: 
thumbStyle: default
---


![P1223 排队接水][1]

```python
    n = int(input())
    list1 = list(map(int, input().split()))
    c = 1
    sum1 = 0
    list2 = []
    for i in range(n):
        list2.append({"id": i + 1, "time": list1[i]})
    list2.sort(key=lambda rank: rank["time"])
    for i in list2:
        sum1 += i["time"] * (n - c)
        c += 1
    for i in range(n):
        if i == n - 1:
            print(list2[i]["id"], end="")
        else:
            print(list2[i]["id"], end=" ")
    print()
    print("%.2f" % (sum1/n))
```

  [1]: https://i.loli.net/2021/06/02/kzh7MsgTyiPWaUK.png