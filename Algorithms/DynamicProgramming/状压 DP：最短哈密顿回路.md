# 最短哈密顿回路

## 代码

时间复杂度 $\Theta(n^2 2^n)$。

```cpp
#include <bits/stdc++.h>
#define popcount __builtin_popcount
using namespace std;
typedef long long ll;
typedef unsigned int uint;

template<typename T>
void chkmin(T &x, T y) {
    x = min(x, y);
}

const int N = 20;

int n;
int dis[N][N];

int f[1 << N][N];

int main() { ios::sync_with_stdio(0); cin.tie(0);
    cin >> n;
    for (int i = 0; i < n; i++)
        for (int j = 0; j < n; j++)
            cin >> dis[i][j];

    uint tot = (1 << n) - 1;
    memset(f, 0x3f, sizeof f);
    f[1][0] = 0;
    for (uint u = 0; u <= tot; u++)
        for (int i = 0; i < n; i++)
            if (u & (1 << i))
                for (int j = 0; j < n; j++)
                    if ((u ^ (1 << i)) & (1 << j))
                        chkmin(f[u][i], f[u ^ (1 << i)][j] + dis[j][i]);

    int ans = INT_MAX;
    for (int i = 0; i < n; i++)
        chkmin(ans, f[tot][i] + dis[i][0]);
    cout << ans << endl;
    return 0;
}
```

## 模板题目

[P1171 售货员的难题](https://www.luogu.com.cn/problem/P1171)
