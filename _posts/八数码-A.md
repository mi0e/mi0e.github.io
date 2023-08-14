---
title: 八数码(A*)
date: 2023-04-04 19:19:45
categories: 
  - 算法
  - C/C++
tags: 
  - 算法
---

```cpp
#include <bits/stdc++.h>
using namespace std;

int f(string state){
    int res = 0;
    for (int i = 0; i < state.length(); i++)
        if (state[i] != 'x') {
            int t = state[i] - '1';
            res += abs(i / 3 - t / 3) + abs(i % 3 - t % 3);
        }

    return res;
}

string bfs(string start){
    int dx[] = {-1, 0, 1, 0};
    int dy[] = {0, 1, 0, -1};
    char op[] = {'u', 'r', 'd', 'l'};
    string ed = "12345678x";
    unordered_map<string, int> dist;
    unordered_map<string, pair<string, char>> pre;
    priority_queue<pair<int, string>, vector<pair<int, string>>, greater<pair<int, string>>> heap;
    
    heap.push({f(start), start});
    dist[start] = 0;
    
    while (heap.size()) {
        auto t = heap.top();
        heap.pop();
        
        string src = t.second;
        if (src == ed) break;
        
        int x, y;
        for (int i = 0; i < 9; i++)
            if (src[i] == 'x') {
                x = i / 3, y = i % 3;
                break;
            }

        for (int i = 0; i < 4; i++) {
            int tx = x + dx[i];
            int ty = y + dy[i];
            if (tx < 0 || tx >= 3 || ty < 0 || ty >= 3) continue;
            string state = src;
            swap(state[x * 3 + y], state[tx * 3 + ty]);
            if (dist.count(state) == 0 || dist[state] > dist[src] + 1) {
                dist[state] = dist[src] + 1;
                pre[state] = {src, op[i]};
                heap.push({dist[state] + f(state), state});
            }
        }
    }
    
    string res = "";
    while (start != ed) {
        res += pre[ed].second;
        ed = pre[ed].first;
    }
    reverse(res.begin(), res.end());
    
    return res;
}

int main(){
    string g, seq;
    char c;
    
    while (cin >> c) {
        g += c;
        if (c != 'x') seq += c;
    }
    int t = 0;
    for (int i = 0; i < seq.length(); i++) 
        for (int j = i + 1; j < seq.length(); j++)
            if (seq[i] > seq[j]) t++;
    
    if (t % 2) cout << "unsolvable" << endl;
    else cout << bfs(g) << endl;
    
    return 0;
}
```