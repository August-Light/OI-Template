# Dinic 网络最大流

## 代码

```cpp
#include <bits/stdc++.h>
#define rep(i, l, r) for (int i = (l); i <= (r); i++)
#define per(i, r, l) for (int i = (r); i >= (l); i--)
using namespace std;
typedef long long ll;

const int MAXN = 200 + 5;
const int MAXM = 5e3 + 5;
const ll INF = 1e12;

int n, m, s, t;
vector<pair<int, int>> G[MAXN];
ll c[MAXM * 2], f[MAXM * 2];
int level[MAXN], cur[MAXN];

bool bfs() {
    fill(level+1, level+n+1, 0);
    queue<int> q;
    level[s] = 1, q.push(s);
    while (!q.empty()) {
        int u = q.front(); q.pop();
        for (auto [v, i] : G[u]) {
            if (!level[v] && c[i] > f[i]) {
                level[v] = level[u] + 1;
                q.push(v);
            }
        }
    }
    return level[t] != 0;
}
ll dfs(int u, ll flow) {
    if (u == t)
        return flow;
    ll tmp = flow;
    for (int &idx = cur[u]; idx < int(G[u].size()); idx++) {
        auto [v, i] = G[u][idx];
        if (level[v] != level[u] + 1)
            continue;
        ll t = dfs(v, min(tmp, c[i] - f[i]));
        f[i] += t;
        f[i ^ 1] -= t;
        tmp -= t;
        if (tmp == 0)
            break;
    }
    return flow - tmp;
}
ll dinic() {
    ll ans = 0;
    while (bfs()) {
        fill(cur+1, cur+n+1, 0);
        ans += dfs(s, INF);
    }
    return ans;
}

int main() { ios::sync_with_stdio(0); cin.tie(0);
    cin >> n >> m >> s >> t;
    rep(i, 1, m) {
        int u, v, w; cin >> u >> v >> w;
        G[u].emplace_back(v, i << 1), c[i << 1] = w;
        G[v].emplace_back(u, i << 1 | 1);
    }
    cout << dinic() << '\n';
    return 0;
}
```

## 模板题目

[P3376 【模板】网络最大流](https://www.luogu.com.cn/problem/P3376)

[B3606 [图论与代数结构 501] 网络流_1](https://www.luogu.com.cn/problem/B3606)

[B3607 [图论与代数结构 502] 网络流_2](https://www.luogu.com.cn/problem/B3607)

## debug

边的数组要开两倍。

addedge 时是把 `c[i << 1] = w` 而不是 `c[i] = w`。

三个函数都要写返回值。

建模题要记得给 $n,s,t$ 赋值。