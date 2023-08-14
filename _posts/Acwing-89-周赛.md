---
title: Acwing 89周赛
date: 2023-02-14 20:47:16
math: true
tags: 
  - 算法
categories: 
  - C/C++
  - 算法
---


# 满足的数

枚举

```cpp
#include <bits/stdc++.h>
using namespace std;
const int N = 105;

int n, s, a[N];

int main(){
    cin >> n;
    
    for (int i = 0; i < n; i++) cin >> a[i], s += a[i];
    
    int cnt = 0;
    for (int i = 1; i <= 5; i++)
        if ((s + i) % (n + 1) != 1) cnt++;
    cout << cnt;
    
    return 0;
}
```

# 构造矩阵

数据范围很小，直接暴力模拟，时间复杂度 $O(n^3)$

```cpp
#include <bits/stdc++.h>
using namespace std;
const int N = 105;

int n, m;
int a[N][N];
bool st[N][N];

int main(){
    cin >> m >> n;
    
    for (int i = 1; i <= m; i++)
        for (int j = 1; j <= n; j++){
        cin >> a[i][j];
        if (!a[i][j]) {
            for (int k = 1; k <= n; k++) st[i][k] = true;
            for (int k = 1; k <= m; k++) st[k][j] = true;
        } 
    }
    
    if (m == 1 && n == 1 && a[1][1] == 0) {
        cout << "YES\n0" << endl;
        return 0;
    }
    
    for (int i = 1; i <= m; i++)
        for (int j = 1; j <= n; j++) {
        bool isAll = true;
        int cnt;
        if (st[i][j]) cnt = 1;
        else cnt = 0;
        if (a[i][j]) {
            for (int k = 1; k <= n; k++) if (k != j && st[i][k]) cnt++;
            for (int k = 1; k <= m; k++) if (k != i && st[k][j]) cnt++;
        }  
        if (cnt == m + n - 1) isAll = false;
        if (!isAll) {
            cout << "NO";
            return 0;
        }
    }
    
    cout << "YES" << endl;
    for (int i = 1; i <= m; i++) {
        for (int j = 1; j <= n; j++) {
            if (st[i][j]) cout << 0 << " ";
            else cout << 1 << " ";
        }
        cout << endl;
    }
    
    
    return 0;
}
```

# 加减乘

贪心+dp，时间复杂度 $O(n)$

数据范围很大，要注意开LL

`dp[i]`可以从三个状态转移过来

1. `dp[j] + 1`
2. `dp[j] * 2`
3. `dp[j] * 2 - 1`（乘过头退一步，所以代价为两步 $w + x + y$ ）

```cpp
#include <bits/stdc++.h>
using namespace std;
const int N = 1e7 + 10;

int n, x, y;
long long dp[N];

int main(){
    cin >> n >> x >> y;
    
    dp[1] += x;
    for (int i = 2; i <= n; i++) {
        dp[i] = dp[i - 1] + x;
        if (i % 2 == 0) dp[i] = min(dp[i], dp[i / 2] + y);
        else dp[i] = min(dp[i], dp[(i + 1) / 2] + y + x);
    }
    
    cout << dp[n];
    
    return 0;
}
```
