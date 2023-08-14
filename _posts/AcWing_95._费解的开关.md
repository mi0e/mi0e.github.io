---
layout: post
cid: 153
title: AcWing 95. 费解的开关
slug: 153
date: 2022/12/21 19:02:00
updated: 2022/12/21 19:05:15
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


你玩过“拉灯”游戏吗？

**25** 盏灯排成一个 **5**×**5** 的方形。

每一个灯都有一个开关，游戏者可以改变它的状态。

每一步，游戏者可以改变某一个灯的状态。

游戏者改变一个灯的状态会产生连锁反应：和这个灯上下左右相邻的灯也要相应地改变其状态。

我们用数字 **1** 表示一盏开着的灯，用数字 **0** 表示关着的灯。

下面这种状态

```
10111
01101
10111
10000
11011
```

在改变了最左上角的灯的状态后将变成：

```
01111
11101
10111
10000
11011
```

再改变它正中间的灯后状态将变成：

```
01111
11001
11001
10100
11011
```

给定一些游戏的初始状态，编写程序判断游戏者是否可能在 **6**6 步以内使所有的灯都变亮。

#### 输入格式

第一行输入正整数 **n**，代表数据中共有 **n** 个待解决的游戏初始状态。

以下若干行数据分为 **n** 组，每组数据有 **5** 行，每行 **5** 个字符。

每组数据描述了一个游戏的初始状态。

各组数据间用一个空行分隔。

#### 输出格式

一共输出 **n** 行数据，每行有一个小于等于 **6** 的整数，它表示对于输入数据中对应的游戏状态最少需要几步才能使所有灯变亮。

对于某一个游戏初始状态，若 **6** 步以内无法使所有灯变亮，则输出 **−1**。

#### 数据范围

**0**<**n**≤**500**

#### 输入样例：

```
3
00111
01011
10001
11010
11100

11101
11101
11110
11111
11111

01111
11111
11111
11111
11111
```

输出样例：

```
3
2
-1
```

```cpp
#include<bits/stdc++.h>
using namespace std;

int light[7][7], backup[7][7];

void turn(int x, int y){
	backup[x][y] = !backup[x][y];
	backup[x - 1][y] = !backup[x - 1][y];
	backup[x][y - 1] = !backup[x ][y - 1];
	backup[x + 1][y] = !backup[x + 1][y];
	backup[x][y + 1] = !backup[x][y + 1];
}

int main(){
	int n;
	string str;
	str.resize(7);
	scanf("%d", &n);
	for(int i = 0; i < n; i++){
		int res = 10;

		for(int x = 1; x <= 5; x++){
			string str;
			scanf("%s", &str[0]);
			for(int y = 1; y <= 5; y++)
				light[x][y] = str[y - 1] - '0';
		}
		// 枚举操作而非状态
		// 01001 表示操作第2和第5盏灯
		for(int k = 0; k < 32; k++){
			memcpy(backup, light, sizeof light);
			int step = 0;
			for(int j = 1; j <= 5; j++){
				if((k >> (j - 1)) & 1){
					turn(1, j);
					step++;
				}
			}

			for(int j = 2; j <= 5; j++){
				for(int l = 1; l <= 5; l++){
					if(backup[j - 1][l] == 0){
						turn(j, l);
						step++;
					}
				}
			}
			bool dark = false;
			for(int j = 1; j <= 5; j++){
				if(backup[5][j] != 1){
					dark = true;
					break;
				}
			}
			if(!dark){
				res = min(res, step);
			}

		}
		if(res == 10 || res > 6) res = -1;

		cout << res;
	}

	return 0;
}
```
