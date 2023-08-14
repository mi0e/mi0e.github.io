---
layout: post
cid: 71
title: scanf、cin返回值与连续输入
slug: 71
date: 2021/11/04 19:43:00
updated: 2022/03/27 10:21:09
status: publish
author: mi0e
categories: 
  - 编程
  - Q/A
tags: 
  - 算法
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


`scanf("%d %d", &a, &b);`

* **a** , **b** 都成功读入，返回值为 **2**
* 只有 **a** 成功读入，返回值为 **1**
* **a** 和 **b** 都未成功读入，返回值为 **0**
* 遇到 **错误** 或遇到 **end of file**，返回值为 **EOF**

`std::cin >> a >> b; 	// cin 无返回值`

**连续输入参考模板：**

```cpp
while(scanf("%d", &i) != EOF){...}

while(cin >> i){...}
```
