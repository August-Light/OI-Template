# 01BFS

## 代码

时间复杂度 $O(n + m)$。

```cpp
int dis[MAXN];
deque<int> dq;
bool vis[MAXN];
void dijkstra(int s) {
    rep(u, 1, n)
        dis[u] = INF;
    dis[s] = 0, dq.push_back(s);
    while (!dq.empty()) {
        int u = dq.front(); dq.pop_front();
        if (vis[u]) continue;
        vis[u] = true;
        for (auto [v, w] : G[u]) {
            if (dis[v] > dis[u] + w) {
                dis[v] = dis[u] + w;
                if (w == 1)
                    dq.push_back(v);
                else
                    dq.push_front(v);
            }
        }
    }
}
```

## 注

没找到板子题，有个应用：[[ABC077D] Small Multiple](https://www.luogu.com.cn/problem/AT_arc084_b)