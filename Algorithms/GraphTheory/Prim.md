# Prim

## 代码

时间复杂度 $O(m \log m)$。

```cpp
ll dis[MAXN];
bool vis[MAXN];
priority_queue<pii, vector<pii>, greater<pii>> pq;
pair<int, ll> Prim() {
    int tot = 0;
    ll ans = 0;
    for (int u = 1; u <= n; u++)
        dis[u] = INF;
    dis[1] = 0; pq.emplace(0, 1);
    while (!pq.empty()) {
        auto [d, u] = pq.top(); pq.pop();
        if (vis[u]) continue;
        vis[u] = 1; tot++;
        ans += dis[u];
        for (auto [v, w] : G[u])
            if (dis[v] > w) {
                dis[v] = w;
                pq.emplace(dis[v], v);
            }
    }
    return {(tot == n), ans};
}
```

## 注

使用了 C++17 的语法（结构化绑定）：`for (auto [v, w] : G[u])`。

`Prim` 函数返回值意义如下：

```cpp
auto [flg, ans] = Prim();
if (flg)
    cout << ans << endl; // 最小生成树上的边权之和
else
    cout << "orz" << endl; // 不存在最小生成树
```

当 $m$ 与 $n^2$ 同级时，时间复杂度会退化为 $O(n^2 \log n)$。此时应选择无堆优化的朴素 Prim 算法（时间复杂度 $O(n^2 + m)$）。

## 模板题目

[P3366 【模板】最小生成树](https://www.luogu.com.cn/problem/P3366)