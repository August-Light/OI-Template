# SPFA

## 代码

时间复杂度 $O(nm)$。

```cpp
ll dis[MAXN];
queue<int> q;
bool inq[MAXN];
int cnt[MAXN];
bool SPFA(int s) {
    fill(dis, dis+n+1, INF);
    dis[s] = 0;
    q.push(s), inq[s] = 1, cnt[s]++;
    while (!q.empty()) {
        int u = q.front(); q.pop(), inq[u] = 0;
        for (auto [v, w] : G[u]) {
            if (dis[v] > dis[u] + w) {
                dis[v] = dis[u] + w;
                if (!inq[v])
                    q.push(v), inq[v] = 1, cnt[v]++;
                if (cnt[v] == n+1)
                    return true;
            }
        }
    }
    return false;
}
```

## 注

使用了 C++17 的语法（结构化绑定）：`for (auto [v, w] : G[u])`。

这份代码通过判入队次数来判负环。

`SPFA` 函数的返回值为 $1$ 说明有负环，为 $0$ 说明无负环。

## 模板题目

[P3371 【模板】单源最短路径（弱化版）](https://www.luogu.com.cn/problem/P3371)

[P3385 【模板】负环](https://www.luogu.com.cn/problem/P3385)

[P5960 【模板】差分约束](https://www.luogu.com.cn/problem/P5960)

## debug

- `if (cnt[v] == n + 1)` 时才是有负环，而非 `if (cnt[v] == n)`。
- `dis[s]` 要设 $0$。
- `inq` 有没有和 `q` 的操作同步进行？