---
layout: post
cid: 156
title: stringstream 字符串转 int/double
slug: 156
date: 2022/12/27 20:29:00
updated: 2022/12/27 20:31:59
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


某涉密单位下发了某种票据，并要在年终全部收回。

每张票据有唯一的ID号。

全年所有票据的ID号是连续的，但ID的开始数码是随机选定的。

因为工作人员疏忽，在录入ID号的时候发生了一处错误，造成了某个ID断号，另外一个ID重号。

你的任务是通过编程，找出断号的ID和重号的ID。

假设断号不可能发生在最大和最小号。

#### 输入格式

第一行包含整数 **N**，表示后面共有 **N** 行数据。

接下来 **N** 行，每行包含空格分开的若干个（不大于100个）正整数（不大于100000），每个整数代表一个ID号。

#### 输出格式

要求程序输出1行，含两个整数 **m**,**n**用空格分隔。

其中，**m**表示断号ID，**n**表示重号ID。

#### 数据范围

**1**≤**N**≤**100**

#### 输入样例：

```
2
5 6 8 11 9 
10 12 9
```

#### 输出样例：

```
7 9
```

#### AC代码

```cpp
#include <bits/stdc++.h>
using namespace std;

int a[10001];
int c, n;

int main(){
	cin >> n;
	string line;
	getline(cin, line);	\\ cin 会读取换行符
	while(n--){
		getline(cin, line);
		stringstream ssin(line);
		while(ssin >> a[c]){
			c++;
		}
	}
	sort(a, a + c);
	int r1, r2;
	for(int i = 1; i < c; i++){
		if(a[i] == a[i - 1]) r1 = a[i];
		if(a[i] - 2 == a[i - 1]) r2 = a[i] - 1;
	}
	cout << r2 << " " << r1;

	return 0;
}
```

#### stringstream技巧：

##### 转int/double

```c++
string result = "10000";	// double 同理, result = "1.5";
stringstream stream(result);	// 可以是字符串也可以是数字，总之后面直接输入到目标变量里面
int n = 0;
stream >> n;	//n 等于10000
```

##### 转int/double数组

`stringstream`以空格作为分隔符

```c++
string str = "1 2 3 4 5";	// double 同理
stringstream ssin(str);
int i = 0;
int a[10] = {0};
while(ssin >> a[i]) i++;	// 此时a[0] = 1, a[1] = 2 ...
```
