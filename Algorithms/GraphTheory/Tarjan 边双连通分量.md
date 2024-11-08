# Tarjan 边双连通分量

## 代码

时间复杂度 $\Theta(n + m)$。

```cpp
int dfn[MAXN], low[MAXN], cnt;
vector<int> st;
vector<vector<int>> EBCCs;
void Tarjan(int u, int lst) {
    dfn[u] = low[u] = ++cnt;
    st.push_back(u);
    for (auto [v, i] : G[u]) {
        if (i == (lst ^ 1))
            continue;
        if (!dfn[v]) {
            Tarjan(v, i);
            low[u] = min(low[u], low[v]);
        } else
            low[u] = min(low[u], dfn[v]);
    }
    if (dfn[u] == low[u]) {
        vector<int> EBCC;
        int v; do {
            v = st.back(); st.pop_back();
            EBCC.push_back(v);
        } while (v != u);
        EBCCs.push_back(EBCC);
    }
}
```

## 模板题目

[P8436 【模板】边双连通分量](https://www.luogu.com.cn/problem/P8436)