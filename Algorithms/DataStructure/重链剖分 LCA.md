# 重链剖分 LCA

## 代码

时间复杂度 $\Theta(n) - O(\log n)$。

```cpp
int dep[MAXN], siz[MAXN], fa[MAXN], son[MAXN], top[MAXN];
void dfs1(int u, int f) {
    fa[u] = f;
    siz[u] = 1;
    dep[u] = dep[f] + 1;
    for (auto v : G[u]) {
        if (v == fa[u])
            continue;
        dfs1(v, u);
        siz[u] += siz[v];
        if (siz[v] > siz[son[u]])
            son[u] = v;
    }
}
void dfs2(int u, int tp) {
    top[u] = tp;
    if (!son[u]) return;
    dfs2(son[u], tp);
    for (auto v : G[u]) {
        if (v == fa[u])
            continue;
        if (v == son[u])
            continue;
        dfs2(v, v);
    }
}
int LCA(int u, int v) {
    while (top[u] != top[v]) {
        if (dep[top[u]] > dep[top[v]])
            swap(u, v);
        v = fa[top[v]];
    }
    if (dep[u] > dep[v])
        swap(u, v);
    return u;
}
```

## 模板题目

[P3379 【模板】最近公共祖先（LCA）](https://www.luogu.com.cn/problem/P3379)

## debug

记得调用预处理。

`LCA` 中是跳**链头深度**大的节点，而不是跳**深度**大的节点。

`dfs2` 中叶子节点要及时 `return`。