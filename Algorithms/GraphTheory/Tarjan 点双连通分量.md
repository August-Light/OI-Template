# Tarjan 点双连通分量

## 代码

时间复杂度 $\Theta(n + m)$。

```cpp
int dfn[MAXN], low[MAXN], cnt;
vector<int> st;
vector<vector<int>> vbccs;
void Tarjan(int u, int lst) {
    dfn[u] = low[u] = ++cnt;
    st.push_back(u);
    for (auto [v, i] : G[u]) if (i != (lst ^ 1)) {
        if (!dfn[v]) {
            Tarjan(v, i);
            low[u] = min(low[u], low[v]);
            if (low[v] >= dfn[u]) {
                vector<int> vbcc; vbcc.push_back(u);
                int p; do {
                    p = st.back(), st.pop_back();
                    vbcc.push_back(p);
                } while (p != v);
                vbccs.push_back(vbcc);
            }
        } else
            low[u] = min(low[u], dfn[v]);
    }
    if (G[u].empty()) {
        vector<int> vbcc; vbcc.push_back(u);
        vbccs.push_back(vbcc);
    }
}
```

## 模板题目

[P8435 【模板】点双连通分量](https://www.luogu.com.cn/problem/P8435)

## debug

- 特判孤立点。
- 特判自环。加边的时候就不要加自环进来。
- 是 `low[v] >= dfn[u]`。
  - 要加入 `u`。
  - 是 `p != v` 而不是 `p != u`。
- 圆方树开两倍空间。