---
title: 计数DP
date: 2023-08-02 19:01:19
tags:
---

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int k, n;
    cin >> n >> k;
    vector<int> nums;
    while (n) nums.push_back(n % 10), n /= 10;
    reverse(nums.begin(), nums.end());

    int res = 0;
    for (int i = 0; i < nums.size(); i++) {
        int x = nums[i];
        int a = 0, b = 0, c = 1;
        for (int j = 0; j < i; j++) a = a * 10 + nums[j];
        for (int j = i + 1; j < nums.size(); j++) {
            b = b * 10 + nums[j];
            c *= 10;
        }
        if (k)
            if (x < k) res += a * c;
            else if (x == k) res += a * c + b + 1;
            else res += (a + 1) * c;
        else {
            if (x) res += a * c;
            else res += (a - 1) * c + b + 1;
        }
    }
    
    cout << res << endl;

    return 0;
}
```
