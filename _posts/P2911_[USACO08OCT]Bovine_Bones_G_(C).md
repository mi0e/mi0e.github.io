---
layout: post
cid: 54
title: P2911 [USACO08OCT]Bovine Bones G (C)
slug: 54
date: 2021/10/01 20:40:00
updated: 2021/10/01 20:41:00
status: publish
author: mi0e
categories: 
  - 编程
  - 算法
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


![image.png](https://i.loli.net/2021/10/01/dcA2xWtmfYQRaqD.png)

```cpp
/*
	根据题意，总共3个骰子，每个骰子有 S个面，因为数据范围较小，可以直接选择暴力
	每次总和记录到相应的结构体(Sum = 10 -> struct[10])，结构体中保存两个数据：总和(num)、次数(times) 
	最后使用快排(qsort)筛出次数(times)最小的目标 
*/ 

#include<stdio.h>

struct A{		// 声明结构体，存放点数总和与次数 
	int num;
	int times;
};

int compare(const void *a, const void *b){
	struct A *p1 = (struct A *)a;
	struct A *p2 = (struct A *)b;
	if(p1->times == p2->times) return p1->num - p2->num;		// 题意：如果出现概率一样时输出最小总和 
	return p2->times - p1->times;
}

int main(void){
	int s1, s2, s3, s, i, j, k;
	struct A a[80];
	scanf("%d %d %d", &s1, &s2, &s3);
	for(i = 0; i < 81; i++){
		 a[i].times = 0;
		 a[i].num = 0;
	}
	for(i = 1; i <= s1; i++)
		for(j = 1; j <= s2; j++)
			for(k = 1; k <= s3; k++){
				a[i + j + k].num = i + j + k;
				a[i + j + k].times++;
			}

	qsort(a, 80, sizeof(struct A), compare);
	printf("%d", a[0].num);

	return 0;
}
```
