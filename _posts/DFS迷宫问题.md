---
layout: post
cid: 73
title: DFS迷宫问题
slug: 73
date: 2021/11/08 14:36:00
updated: 2022/03/27 10:20:42
status: publish
author: mi0e
categories: 
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


```cpp
#include<bits/stdc++.h>
#pragma GCC optimize(2)
using namespace std;

int m[101][101];
int xS, yS, xE, yE;
int s;

void dfs(int x, int y){
	if(x == xE && y == yE){
		s++;
		return;
	}else{		// 遍历四个方向 
		m[x][y] = 0;
		if(m[x + 1][y]){
			m[x + 1][y] = 0;		// 占位，防止死循环 
			dfs(x + 1, y);
			m[x + 1][y] = 1;
		}
		if(m[x - 1][y]){
			m[x - 1][y] = 0;
			dfs(x - 1, y);
			m[x - 1][y] = 1;
		}
		if(m[x][y + 1]){
			m[x][y + 1] = 0;
			dfs(x, y + 1);
			m[x][y + 1] = 1;
		}
		if(m[x][y - 1]){
			m[x][y - 1] = 0;
			dfs(x, y - 1);
			m[x][y - 1] = 1;
		}
	}
}

int main(void){
	ios::sync_with_stdio(false);
	int x, y, k, Ox, Oy;
	cin >> x >> y >> k;
	for(int i = 1; i <= x; i++)	// 棋盘预定义
		for(int j = 1; j <= y; j++)
			m[i][j] = 1;
	cin >> xS >> yS >> xE >> yE;
	for(int i = 0; i < k; i++){	// 预先写入障碍
		cin >> Ox >> Oy;
		m[Ox][Oy] = 0;
	}
	dfs(xS, yS);
	cout << s;

	return 0;
} 
```
