---
layout: post
cid: 74
title: Map 单词分析
slug: 74
date: 2021/11/08 15:30:00
updated: 2022/03/27 10:19:47
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


**蓝桥杯无法使用`for(x : y){}` 、 `auto`等的C11语法和关键字**

```cpp
#include<bits/stdc++.h>
using namespace std;

map<char, int> m;

int main(void){
	string str;
	char mc;
	int s = 0;
	for(int i = 97; i <= 122; i++){
		m.insert(make_pair((char)i, 0));
	}
	cin >> str;
	for(int i = 0; i < str.size(); i++){
		m[str[i]]++;
	}
	for(map<char, int>::iterator i = m.begin(); i != m.end(); i++){
		if(s < i->second) mc = i->first, s = i->second;		// 记录次数
	}
	cout << mc << endl << m[mc];

	return 0;
}
```
