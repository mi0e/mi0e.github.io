---
layout: post
cid: 164
title: gcd与欧拉质数筛模板
slug: 164
date: 2023/01/10 16:04:00
updated: 2023/01/10 21:33:45
status: publish
author: mi0e
categories: 
  - 算法
tags: 
  - 数论
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
math: true
---


## 欧几里得辗转相除法

$gcd(a, b)=gcd(b,a\ mod\ b)=···=gcd(n,0)$

```cpp
int gcd(int a, int b){
    return b ? gcd(b, a % b) : a;
}
```

## 扩展gcd

对任意整数 $a, b$ 都存在非零 $x, y$ , 有 $ax + by = gcd(a, b)$ , 且 $x,y$ 通解为 ：

$$ \left\{
\begin{aligned}
x & =  x - \frac bd \\
y & =  y + \frac ad \\
\end{aligned}
\right.
$$

### 裴蜀定理

判断 $x, y$ 在 $ax + by = c$ 下是否存在 $a, b$

只需要满足 $c \% gcd(x, y) == 0$ 

```cpp
int exgcd(int a, int b, int &x, int &y){
    if (!b) {
        x = 1, y = 0;
        return a;
    }
    int d = exgcd(b, a % b, y, x);
    y -= a / b * x;
    
    return d;
}
```

### 线性同余（扩展欧几里得）

求关于 $x$ 的同余方程 $ax≡1(mod \ b)$ 的最小正整数解。

```cpp
#include <bits/stdc++.h>
using namespace std;

int exgcd(int a, int b, int &x, int &y){
    if (!b) {
        x = 1, y = 0;
        return a;
    }
    int d = exgcd(b, a % b, y, x);
    y -= a / b * x;
    
    return d;
}

int main(){
    int a, b, x, y;
    cin >> a >> b;
    
    int d = exgcd(a, b, x, y);
    
    cout << ((x / d) % b + b) % b;
    
    return 0;
}
```

## 欧拉质数筛

#### 时间复杂度$O(n)$

```cpp
const int N = 1e8 + 10;
int p[N], cnt;
bool st[N];
void get_primes(int n){
    for(int i = 2; i <= n; i++){
        if(!st[i]) p[cnt++] = i;
        for(int j = 0; i * p[i] <= n; j++){
            st[p[j] * i] = true;
            if(i % p[j] == 0) break;
        }
    }
}
```
