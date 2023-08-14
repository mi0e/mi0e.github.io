---
layout: post
cid: 62
title: c_str()使用方法
slug: 62
date: 2021/10/26 21:52:15
updated: 2021/10/26 21:52:15
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


```cpp
//标准库的string类提供了三个成员函数来从一个string得到c类型的字符数组
//c_str()：生成一个const char*指针，指向以空字符终止的数组。
#include <bits/stdc++.h>
using namespace std;
 
int main()
{
    //string-->char*
    //c_str()函数返回一个指向正规C字符串的指针, 内容与本string串相同
    //这个数组的数据是临时的，当有一个改变这些数据的成员函数被调用后，其中的数据就会失效。
    //因此要么现用先转换，要么把它的数据复制到用户自己可以管理的内存中
    const char *c;
    string s = "1234";
    c = s.c_str();
    cout<<c<<endl;
    s = "abcde";
    cout<<c<<endl;
}
```

输出：

```
1234
abcde
```
