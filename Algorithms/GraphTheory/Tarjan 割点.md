# Tarjan 割点

## 代码

时间复杂度 $\Theta(n + m)$。

```cpp
int dfn[MAXN], low[MAXN], cnt;
bool cut[MAXN];
void Tarjan(int u, int lst) {
    dfn[u] = low[u] = ++cnt;
    int son = 0;
    for (auto [v, i] : G[u]) {
        if (i == (lst ^ 1)) continue;
        if (!dfn[v]) {
            son++;
            Tarjan(v, i);
            low[u] = min(low[u], low[v]);
            if (low[v] >= dfn[u])
                cut[u] = 1;
        } else
            low[u] = min(low[u], dfn[v]);
    }
    if (lst == 0 && son < 2)
        cut[u] = 0;
}
```

## 模板题目

[P3388 【模板】割点（割顶）](https://www.luogu.com.cn/problem/P3388)