---
layout: post
cid: 72
title: C++ STL中的next_permutation
slug: 72
date: 2021/11/05 14:45:00
updated: 2022/03/27 10:21:03
status: publish
author: mi0e
categories: 
  - C/C++
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


> Rearranges the elements in the range `[first,last)` into the next *[lexicographically](https://cplusplus.com/lexicographical_compare) greater* permutation.
>
> *将范围内的元素重新排列`[first,last)`为下一个[字典序](https://cplusplus.com/lexicographical_compare)更大的排列。*
>
> [--cplusplus.com](https://cplusplus.com)

对于next_permutation函数，其函数原型为：

```
 #include <algorithm>
 bool next_permutation(iterator start,iterator end)
```

如下例子：

```cpp
#include <iostream>
#include <algorithm>
using namespace std;
int main(){
    int num[3]={1, 2, 3};
    do{
        cout << num[0] << " " << num[1] << " " << num[2] << endl;
    }while(next_permutation(num, num + 3));
    return 0;
}

输出结果：
1 2 3
1 3 2
2 1 3
2 3 1
3 1 2
3 2 1
```

当我们把`while(next_permutation(num, num + 3))`中的`3`改为`2`时，输出就变为了：

```
1 2 3
2 1 3
```

由此可见，next_permutation是对数组前n项进行全排列

同理，既然有下一个全排列函数，那肯定是有上一个全排列函数：`prev_permutation`使用方法与`next_permutation`一致。
