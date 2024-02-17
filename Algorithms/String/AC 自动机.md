# AC 自动机

## 代码

时间复杂度 $\Theta(n |\Sigma| + m)$。

空间复杂度 $\Theta(n |\Sigma| + m)$。

$n$ 为模式串长度之和，$m$ 为文本串长度。

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;

const int MAXN = 2e5 + 5; // 模式串长度之和

int tr[MAXN][26], fail[MAXN], tot = 0;
int e[MAXN], sum[MAXN];
vector<int> G[MAXN];
int ins(string s) {
    int u = 0;
    for (auto ch : s) {
        int c = ch - 'a';
        if (!tr[u][c])
            tr[u][c] = ++tot;
        u = tr[u][c];
    }
    return u;
}
void bfs() {
    queue<int> q;
    for (int c = 0; c < 26; c++)
        if (tr[0][c])
            q.push(tr[0][c]);
    while (!q.empty()) {
        int u = q.front(); q.pop();
        for (int c = 0; c < 26; c++)
            if (tr[u][c]) {
                fail[tr[u][c]] = tr[fail[u]][c];
                q.push(tr[u][c]);
            } else
                tr[u][c] = tr[fail[u]][c];
    }
}

int main() { ios::sync_with_stdio(0); cin.tie(0);
    int n; cin >> n; for (int i = 1; i <= n; i++) {
        string s; cin >> s;
        e[i] = ins(s);
    }
    bfs();
    for (int u = 1; u <= tot; u++)
        G[fail[u]].push_back(u);

    string t; cin >> t;
    int u = 0;
    for (auto ch : t) {
        int c = ch - 'a';
        u = tr[u][c];
        sum[u]++;
    }
    auto dfs = [&](int u, auto&& self) -> void {
        for (auto v : G[u]) {
            self(v, self);
            sum[u] += sum[v];
        }
    };
    dfs(0, dfs);
    for (int i = 1; i <= n; i++)
        cout << sum[e[i]] << '\n';
    return 0;
}
```

## 注

是 P5357 完整代码。

## 模板题目

[P5357 【模板】AC 自动机](https://www.luogu.com.cn/problem/P5357)