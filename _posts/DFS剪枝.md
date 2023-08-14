---
title: DFS剪枝
date: 2023-03-15 13:40:02
categories: 
  - 算法
  - C/C++
tags: 
  - 算法
---

# 剪枝技巧

1. 可行性剪枝
2. 最优性剪枝
3. 排除等效冗余
4. 优化搜索顺序
5. 记忆化搜索（动态规划）

# 小猫爬山

```cpp
#include <bits/stdc++.h>
using namespace std;
const int N = 20;

int ans = N;
int n, w;
int c[N];
int s[N];

void dfs(int cat, int car){
    if (car >= ans) return;         // 最优性剪枝
    if (cat == n) ans = car;
    
    for (int i = 0; i < car; i++)
        if (s[i] + c[cat] <= w) {   // 可行性剪枝
            s[i] += c[cat];
            dfs(cat + 1, car);
            s[i] -= c[cat];
        }
    
    s[car] += c[cat];
    dfs(cat + 1, car + 1);
    s[car] -= c[cat];
}

int main(){
    cin >> n >> w;
    
    for (int i = 0; i < n; i++) cin >> c[i];
    
    sort(c, c + n);
    reverse(c, c + n);
    
    dfs(0, 0);
    
    cout << ans;
    
    return 0;
}
```