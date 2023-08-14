---
layout: post
cid: 63
title: 高精度阶乘模板(C++)
slug: 63
date: 2021/10/27 12:13:00
updated: 2021/10/27 12:17:15
status: publish
author: mi0e
categories: 
  - C/C++
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
#include<bits/stdc++.h>
using namespace std;
const int MAX = 10000;
struct N{
	int len;
	int a[MAX];
	N(int x = 0){		// 初始化
		memset(a, 0, sizeof(a));
		for(len = 1; x; len++){
			a[len] = x % 10;
			x /= 10;
		}
	}
	void f(int _l){		// 进位
		len = _l;
		for(int i = 1; i <= len; i++){
			a[i + 1] += a[i] / 10;
			a[i] %= 10;
		}
		for(;!a[len];) len--;		// 去除无效前置0
	}
	void print(){
		for(int i = max(len, 1); i >= 1; i--)
			printf("%d", a[i]);
	}
	int &operator[](int i){		// 重载[]，方便直接使用Node[num]访问Node数组
		return a[i];
	}
	N operator*(int t){		// 重载*
		N c;
		for(int i = 1; i <= len; i++)
			c[i] = a[i] * t;
		c.f(len + 11);
		return c;
	}
};

int main(void){
	N fac(1);
	int n;
	cin >> n;
	for(int i = 1; i <= n; i++)
		fac = fac * i; 
	fac.print();

	return 0;
}
```
