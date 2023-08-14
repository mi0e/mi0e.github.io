---
layout: post
cid: 169
title: KMP
slug: 169
date: 2023/01/30 18:25:00
updated: 2023/01/30 18:28:29
status: publish
author: mi0e
categories: 
  - 算法
  - C/C++
tags: 
customSummary: 
mathjax: auto
noThumbInfoEmoji: 
noThumbInfoStyle: default
outdatedNotice: no
parseWay: auto
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
const int N = 100, M = 1000;

int n, m;
char p[N], s[M];
int ne[N];

int main(){
	cin >> n >> p + 1 >> m >> s + 1;

	for(int i = 2, j = 0; i <= n; i++){
		while(j && p[i] != p[j + 1]) j = ne[j];
		if(p[i] == p[j + 1]) j++;
		ne[i] = j;
	}

	for(int i = 1, j = 0; i <= m; i++){
		while(j && s[i] != p[j + 1]) j = ne[j];
		if(s[i] == p[j + 1]) j++;
		if(j == n){
			printf("%d", i - n);
			break;
		}
	}

	return 0;
}

```
