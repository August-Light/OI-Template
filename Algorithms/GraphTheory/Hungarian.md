# Hungarian

## 代码

时间复杂度 $O(nm)$。

```cpp
int mch[MAXN], vist[MAXN];
bool dfs(int u, int tag) {
    if (vist[u] == tag)
        return false;
    vist[u] = tag;
    for (auto v : G[u]) {
        if (!mch[v] || dfs(mch[v], tag)) {
            mch[v] = u;
            return true;
        }
    }
    return false;
}
```

## 注

完整代码：

```cpp
#include <bits/stdc++.h>
#define rep(i, l, r) for (int i = (l); i <= (r); i++)
#define per(i, r, l) for (int i = (r); i >= (l); i--)
using namespace std;
typedef long long ll;

const int MAXN = 500 + 5;

int n1, n2, m;
vector<int> G[MAXN];

// Paste it here

int main() { ios::sync_with_stdio(0); cin.tie(0);
    cin >> n1 >> n2 >> m;
    rep(i, 1, m) {
        int u, v; cin >> u >> v;
        G[u].push_back(v);
    }

    int ans = 0;
    rep(u, 1, n1)
        if (dfs(u, u))
            ans++;
    cout << ans << '\n';
    return 0;
}
```

## 模板题目

[P3386 【模板】二分图最大匹配](https://www.luogu.com.cn/problem/P3386)