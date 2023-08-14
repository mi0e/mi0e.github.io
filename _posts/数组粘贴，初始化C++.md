---
layout: post
cid: 64
title: 数组粘贴，初始化C++
slug: 64
date: 2021/10/28 11:51:00
updated: 2021/10/28 17:03:35
status: publish
author: mi0e
categories: 
  - 编程
  - C/C++
  - Q/A
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


粘贴：memcpy()

初始化（可初始化结构体内的数组元素）：memset()

```cpp
int a[5];
int b[5] = {1, 2, 3, 4, 5}
memset(a, 0, sizeof(int));	// 把a中所有数组元素初始化为1
memcpy(a, b, 5 * sizeof(int));	// 把b数组覆盖到a数组
```
