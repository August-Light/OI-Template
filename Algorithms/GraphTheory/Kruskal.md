# Kruskal

## 代码

时间复杂度 $O(m \log m)$。

```cpp
struct Edge {
    int u, v;
    ll w;
    Edge(int u, int v, ll w) : u(u), v(v), w(w) {}
};

int n, m;
vector<Edge> edges;

pair<bool, ll> kruskal() {
    sort(edges.begin(), edges.end(), [](Edge &A, Edge &B) {
        return A.w < B.w;
    });
    ll ans = 0;
    DSU dsu; dsu.init(n);
    int cnt = 0;
    for (auto [u, v, w] : edges) {
        if (dsu.same(u, v))
            continue;
        dsu.merge(u, v);
        ans += w;
        cnt++;
    }
    if (cnt != n-1)
        return {false, 0};
    return {true, ans};
}
```

## 注

`kruskal` 函数返回值意义如下：

```cpp
auto [flg, ans] = kruskal();
if (flg)
    cout << ans << endl; // 最小生成树上的边权之和
else
    cout << "orz" << endl; // 不存在最小生成树
```

## 模板题目

[P3366 【模板】最小生成树](https://www.luogu.com.cn/problem/P3366)