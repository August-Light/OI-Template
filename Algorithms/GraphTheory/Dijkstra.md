# Dijkstra

## 代码

时间复杂度 $O(m \log m)$。

```cpp
ll dis[MAXN];
priority_queue<pii, vector<pii>, greater<pii>> pq;
bool vis[MAXN];
void Dijkstra(int s) {
    for (int u = 1; u <= n; u++)
        dis[u] = INF;
    dis[s] = 0;
    pq.emplace(0, s);
    while (!pq.empty()) {
        int u = pq.top().second; pq.pop();
        if (vis[u]) continue;
        vis[u] = 1;
        for (auto [v, w] : G[u])
            if (dis[v] > dis[u] + w) {
                dis[v] = dis[u] + w;
                pq.emplace(dis[v], v);
            }
    }
}
```

## 注

使用了 C++17 的语法（结构化绑定）：`for (auto [v, w] : G[u])`。

当 $m$ 与 $n^2$ 同级时，时间复杂度会退化为 $O(n^2 \log n)$。此时应选择无堆优化的朴素 Dijkstra 算法（时间复杂度 $O(n^2 + m)$）。

用 pbds 优化：

```cpp
ll dis[MAXN];
__gnu_pbds::priority_queue<pii, greater<pii>, thin_heap_tag> pq;
bool vis[MAXN];
void Dijkstra(int s) {
    rep(u, 1, n)
        dis[u] = INF;
    dis[s] = 0, pq.push({0, s});
    while (!pq.empty()) {
        int u = pq.top().second; pq.pop();
        if (vis[u]) continue;
        vis[u] = 1;
        for (auto [v, w] : G[u])
            if (dis[v] > dis[u] + w) {
                dis[v] = dis[u] + w;
                pq.push({dis[v], v});
            }
    }
}
```

## 模板题目

[P4779 【模板】单源最短路径（标准版）](https://www.luogu.com.cn/problem/P4779)

## debug

加入源点时不要设置其 `vis`。会导致没有更新其它所有点的最短路。