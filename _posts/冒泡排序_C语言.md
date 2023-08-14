---
layout: post
cid: 53
title: 冒泡排序 C语言
slug: 53
date: 2021/09/11 17:10:00
updated: 2021/09/11 19:30:11
status: publish
author: mi0e
categories: 
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


```cpp
#include<stdio.h>

/* 交换函数
void swap(int *pa, int *pb){
	int temp;
	if(*pa > *pb){
		temp = *pb;
		*pb = *pa;
		*pa = temp; 
	}
}
*/

int main(void){
	int a[] = {1, 3, 5, 2, 14, 8, 4 ,9};
	int i, j;
	int temp;
	int num = (sizeof(a) / sizeof(a[0]));
	printf("排序前：");
	for(i = 0; i < num; i++){
		printf("%d ", a[i]);
	}
	printf("\n");

	// 冒泡 
	for(i = 0; i < num; i++){		// 游标 
		for(j = i; j < num - 1; j++){		// 两两比较 
			if(a[j] > a[j + 1]){
				temp = a[j + 1];
				a[j + 1] = a[j];
				a[j] = temp;
			}
			// swap((a + j), (a + j + 1));
		}
	}

	printf("排序后：");
	for(i = 0; i < num; i++){
		printf("%d ", a[i]);
	}
	return 1;
}
```
