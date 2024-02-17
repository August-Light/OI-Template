# 倍增 LCA

## 代码

时间复杂度 $\Theta(n \log n) - O(\log n)$。

```cpp
int dep[MAXN], anc[MAXN][MAXT];
void dfs(int u, int fa) {
    dep[u] = dep[fa] + 1;
    anc[u][0] = fa;
    for (auto v : G[u]) {
        if (v == fa)
            continue;
        dfs(v, u);
    }
}
void init() {
    for (int j = 1; j <= T; j++)
        for (int u = 1; u <= n; u++)
            anc[u][j] = anc[anc[u][j-1]][j-1];
}
int LCA(int u, int v) {
    if (dep[u] < dep[v])
        swap(u, v);
    for (int j = T; j >= 0; j--)
        if (dep[anc[u][j]] >= dep[v])
            u = anc[u][j];
    if (u == v)
        return u;
    for (int j = T; j >= 0; j--)
        if (anc[u][j] != anc[v][j])
            u = anc[u][j], v = anc[v][j];
    return anc[u][0];
}
```

## 注

为了卡常，可以将 `anc` 小的那一维放在前，即 `anc[MAXT][MAXN]`。

## 模板题目

[P3379 【模板】最近公共祖先（LCA）](https://www.luogu.com.cn/problem/P3379)

## debug

记得调用预处理。