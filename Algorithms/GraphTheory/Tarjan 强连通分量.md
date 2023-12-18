# Tarjan 强连通分量

## 代码

时间复杂度 $\Theta(n + m)$。

```cpp
int dfn[MAXN], low[MAXN], cnt;
bool ins[MAXN];
stack<int> st;
vector<vector<int>> SCCs;
void Tarjan(int u) {
    low[u] = dfn[u] = ++cnt;
    st.push(u); ins[u] = 1;
    for (auto v : G[u])
        if (!dfn[v]) {
            Tarjan(v);
            low[u] = min(low[u], low[v]);
        } else if (ins[v])
            low[u] = min(low[u], dfn[v]);

    if (dfn[u] == low[u]) {
        vector<int> SCC;
        int v; do {
            v = st.top(); st.pop(); ins[v] = 0;
            SCC.push_back(v);
        } while (v != u);
        SCCs.push_back(SCC);
    }
}
```

## 模板题目

[P2863 [USACO06JAN]The Cow Prom S](https://www.luogu.com.cn/problem/P2863)

[P3387 【模板】缩点](https://www.luogu.com.cn/problem/P3387)