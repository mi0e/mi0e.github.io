---
layout: post
cid: 69
title: Vector 二分查找
slug: 69
date: 2021/11/04 15:39:00
updated: 2022/03/27 10:21:28
status: publish
author: mi0e
categories: 
  - 编程
  - 算法
  - C/C++
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


二分查找：

* lower_bound：查找第一个大于或等于某个元素的位置。
* upper_bound：查找第一个大于某个元素的位置。

Vector 插入元素

* iterator insert(iterator it, const T& x)：iterator向量中迭代器指向元素前增加一个元素x
* iterator insert(iterator it, int n,const T& x)：向量中迭代器指向元素前增加n个相同的元素x
* iterator insert(iterator it, const_iterator first, const_iterator last)：向量中迭代器指向元素前插入另一个相同类型向量的[first, last)间的数据

```cpp
#include<bits/stdc++.h>
using namespace std;

int main(void){
	vector<int> arr;
	int t, k, a;
	for(int i = 0; i < 9; i++){
		cin >> t;
		arr.push_back(t);
	}
	cin >> k;
	auto pos = upper_bound(arr.begin(), arr.end(), k); 	// vector<int>::iterator
	arr.insert(pos, k);
	for(int i = 0; i < 10; i++)
		cout << arr[i] << endl;

	return 0;
} 
```
