---
title: 多源BFS
date: 2023-03-19 22:18:09
categories: 
  - 算法
  - C/C++
tags: 
  - 算法
---

# 解法

将所有终点的距离置为0，出发点-1或0x3f，并把所有终点放入队列BFS

# 多源BFS

2022蓝桥杯 国赛

稍微有点变换的多源BFS

坑点：一个点可以传送多个点

```cpp
#include <iostream>
#include <queue>
#include <vector>
#include <cstring>
using namespace std;
const int N = 2020;

typedef pair<int, int> PII;
vector<PII> door[N][N];
int dist[N][N], g[N][N];
int n, m;
int x1, y1, x2, y2;
int dx[] = {-1, 0, 1, 0};
int dy[] = {0, 1, 0, -1};
double res;

void bfs(){
    queue<PII> q;
    q.push({n, n});
    while (q.size()) {
        auto t = q.front();
        q.pop();
        int x = t.first, y = t.second;
    
        for (int i = 0; i < 4; i++) {
            int tx = x + dx[i];
            int ty = y + dy[i];
            if (tx < 1 || tx > n || ty < 1 || ty > n) continue;
            if (g[x][y])
                for (auto d : door[x][y]) {
                if (dist[d.first][d.second] > dist[x][y] + 1) {
                    dist[d.first][d.second] = dist[x][y] + 1;
                    q.push({d.first, d.second});
                }
            }
            if (dist[tx][ty] > dist[x][y] + 1) {
                dist[tx][ty] = dist[x][y] + 1;
                q.push({tx, ty});
            }
        }
    }
}

int main()
{
    scanf("%d%d", &n, &m);
    memset(dist, 0x3f, sizeof dist);
    dist[n][n] = 0;
    for (int i = 1; i <= m; i++) {
        scanf("%d%d%d%d", &x1, &y1, &x2, &y2);
        door[x1][y1].push_back({x2, y2});
        door[x2][y2].push_back({x1, y1});
        g[x1][y1] = g[x2][y2] = 1;
    }
  
    bfs();
  
    for (int i = 1; i <= n; i++)
        for (int j = 1; j <= n; j++)
            res += dist[i][j];
  
    printf("%0.2lf", res / (double)(n * n));
  
    return 0;
}
```
