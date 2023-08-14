---
layout: post
cid: 59
title: 历届真题 分糖果【第五届】【省赛】【C组】
slug: 59
date: 2021/10/16 16:35:00
updated: 2021/10/16 16:39:21
status: publish
author: mi0e
categories: 
  - 编程
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


![image.png](http://mioe.xyz/usr/uploads/2021/10/3684429808.png)

```cpp
#include<bits/stdc++.h>
using namespace std;

int eq(int *t, int l){
	for(int i = 1; i < l; i++)
		if(t[0] != t[i]) return 0;
	return 1;
}

int main(void){
	int n, m;
	cin >> n;
	int c[n], i, s = 0, bf[n];		// bf[n] 缓存区 
	for(i = 0; i < n; i++)
		cin >> c[i];
	while(1){						// 思路：每次分糖果，把第i个 分出 的糖果记录到 对应的 缓存区， 
		for(i = 0; i < n; i++){		// 		 第i个小朋友的苹果等于 自身糖果的一半 加  i - 1 缓冲区的糖果 
			c[i] /= 2;				//	例如： 有三个小朋友
			bf[i] = c[i];			//         2 2 4 
		}							// 对半分：1 1 2(1)
		c[0] += bf[n - 1];			//          / / / 
		for(i = 1; i < n; i++)	 	// 缓冲区：1 1 2 
			c[i] += bf[i - 1];		//         | | | 
		for(i = 0; i < n; i++)		// 完成：3 2 3(3) 
			if(c[i] % 2 != 0){
				c[i]++;
				s++;
			}
		if(eq(c, n) == 1) break;
	}

	cout << s;
	return 0;
} 
```
