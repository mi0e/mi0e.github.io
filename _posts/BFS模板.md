---
layout: post
cid: 160
title: BFS模板
slug: 160
date: 2023/01/05 17:40:00
updated: 2023/01/07 14:58:33
status: publish
author: mi0e
categories: 
  - 算法
  - C/C++
tags: 
  - BFS
customSummary: 
mathjax: auto
noThumbInfoEmoji: 
noThumbInfoStyle: default
outdatedNotice: no
parseWay: vditor
reprint: standard
thumb: 
thumbChoice: default
thumbDesc: 
thumbSmall: 
thumbStyle: default
---


#### 题目

字符 E 表示奶酪所在的位置，字符 # 表示墙壁，字符 . 表示可以通行，

对于每一组数据，输出吃到奶酪的最少单位时间。

若无法吃到奶酪，则输出“oop!”（只输出引号里面的内容，不输出引号）。

在 1 个单位时间内可以从当前的位置走到它上下左右四个方向上的任意一个位置，但不能走出地图边界。

#### 模板

###### 二维

```cpp
#include<bits/stdc++.h>
using namespace std;
const int N = 210;

// 方向偏移量
int dx[4] = {-1, 0, 1, 0};
int dy[4] = {0, 1, 0, -1};
// 距离
int dist[N][N];
int n, m;
pair<int, int> start;
pair<int, int> ed;
// 迷宫
char g[N][N];

int bfs(pair<int, int> s, pair<int, int> e){
	queue<pair<int, int>> q;
	memset(dist, -1, sizeof dist);

	dist[s.first][s.second] = 0;						// 起点
	q.push(s);

	while(!q.empty()){
		pair<int, int> t = q.front();
		q.pop();

		if(t == e) return dist[t.first][t.second];			// 判断是否终点

		for(int i = 0; i < 4; i++){
			int x = t.first + dx[i];
			int y = t.second + dy[i];
			if(x < 0 || y < 0 || x >= n || y >= m) continue;	// 越界
			if(g[x][y] == '#') continue;				// 碰墙
			if(dist[x][y] != -1) continue;				// 已遍历

			dist[x][y] = dist[t.first][t.second] + 1;		// 距离加一
			q.push({x, y});
		}
	}

	return -1;
}

int main(){
	int t;
	cin >> t;
	while(t--){
		scanf("%d %d", &n, &m);
		for(int i = 0; i < n; i++) scanf("%s", g[i]);
		for(int i = 0; i < n; i++){
			for(int j = 0; j < m; j++){
				if(g[i][j] == 'S') start = {i, j};
				if(g[i][j] == 'E') ed = {i, j};
			}
		}

		int d = bfs(start, ed);
		if(d == -1) printf("oop!\n");
		else printf("%d\n", d);
	}


	return 0;
}
```

##### 三维

```cpp
#include<bits/stdc++.h>
using namespace std;
const int N = 101;

pair<int, pair<int, int>> start, ed, tmp;
char g[N][N][N];
int st[N][N][N];
int dy[4] = {-1, 0, 1, 0};
int dz[4] = {0, -1, 0, 1};
int l, r, c;

int bfs(pair<int, pair<int, int>> s, pair<int, pair<int, int>> e){
	memset(st, -1, sizeof st);
	queue<pair<int, pair<int, int>>> q;
	st[s.first][s.second.first][s.second.second] = 0;
	q.push(s);

	while(!q.empty()){
		tmp = q.front();
		q.pop();
		if(tmp == e) return st[tmp.first][tmp.second.first][tmp.second.second];
	
		int x = tmp.first, y, z;
	
		if(x + 1 < l && st[x + 1][tmp.second.first][tmp.second.second] == -1 && g[x + 1][tmp.second.first][tmp.second.second] != '#'){
			st[x + 1][tmp.second.first][tmp.second.second] = st[tmp.first][tmp.second.first][tmp.second.second] + 1;
			q.push({x + 1, {tmp.second.first, tmp.second.second}});
		}
		if(x - 1 >= 0 && st[x - 1][tmp.second.first][tmp.second.second] == -1 && g[x - 1][tmp.second.first][tmp.second.second] != '#'){
			st[x - 1][tmp.second.first][tmp.second.second] = st[tmp.first][tmp.second.first][tmp.second.second] + 1;
			q.push({x - 1, {tmp.second.first, tmp.second.second}});
		}
	
		for(int i = 0; i < 4; i++){
			y = tmp.second.first + dy[i];
			z = tmp.second.second + dz[i];
			if(st[x][y][z] != -1) continue;
			if(y < 0 || z < 0 || y >= r || z >= c) continue;
			if(g[x][y][z] == '#') continue;
		
			st[x][y][z] = st[tmp.first][tmp.second.first][tmp.second.second] + 1;
			q.push({x, {y, z}});
		}
	
	
	}

	return -1;
}

int main(){
	while(1){
		cin >> l >> r >> c;
		if(l == 0) break;
		for(int i = 0; i < l; i++)
			for(int j = 0; j < r; j++) 
				scanf("%s", g[i][j]);
	
		for(int i = 0; i < l; i++)
			for(int j = 0; j < r; j++)
				for(int z = 0; z < c; z++)
					if(g[i][j][z] == 'S') start = {i, {j, z}};
					else if(g[i][j][z] == 'E') ed = {i, {j, z}};
	
		int step = bfs(start, ed);
		if(step == -1) printf("Trapped!\n");
		else printf("Escaped in %d minute(s).\n", step);
	}

	return 0;
}
```
