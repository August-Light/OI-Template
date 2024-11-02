# P3455 [POI2007] ZAP-Queries

## 代码

时间复杂度 $\Theta(n) - \Theta(\sqrt n)$。

```cpp
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;

const int MAXN = 5e4 + 5;

vector<int> prime;
bool vis[MAXN];
ll mu[MAXN], summu[MAXN];
void init(int n) {
    vis[1] = 1;
    mu[1] = 1;
    for (int i = 2; i <= n; i++) {
        if (!vis[i]) {
            mu[i] = -1;
            prime.push_back(i);
        }
        for (auto j : prime) {
            int k = i * j; if (k > n) break;
            vis[k] = 1;
            if (i % j == 0) {
                mu[k] = 0;
                break;
            }
            mu[k] = -mu[i];
        }
    }
}

ll solve(int n, int m, int k = 1) {
    if (k != 1) return solve(n / k, m / k);
    if (n > m) swap(n, m);

    ll ret = 0;
    for (ll l = 1, r; l <= n; l = r + 1) {
        ll t1 = n / l, t2 = m / l;
        r = min(n / t1, m / t2);
        ret += t1 * t2 * (summu[r] - summu[l-1]);
    }
    return ret;
}

int main() { ios::sync_with_stdio(0); cin.tie(0);
    init(5e4);
    for (int i = 1; i <= 5e4; i++)
        summu[i] = summu[i-1] + mu[i];

    int T; cin >> T; while (T--) {
        ll n, m, k; cin >> n >> m >> k;
        cout << solve(n, m, k) << endl;
    }
    return 0;
}
```

## 注

$$
\begin{aligned}
& \sum\limits_{i=1}^n \sum\limits_{j=1}^m [\gcd(i,j)=1] \\
=& \sum\limits_{i=1}^n \sum\limits_{j=1}^m \sum\limits_{d|\gcd(i,j)} \mu(d) \\
=& \sum\limits_{i=1}^n \sum\limits_{j=1}^m \sum\limits_{d=1}^n [d|i][d|j] \mu(d) \\
=& \sum\limits_{d=1}^n \mu(d) \sum\limits_{i=1}^n \sum\limits_{j=1}^m [d|i][d|j] \\
=& \sum\limits_{d=1}^n \mu(d) \left\lfloor\dfrac nd \right\rfloor \left\lfloor\dfrac md \right\rfloor
\end{aligned}
$$

## 模板题目

[P3455 [POI2007] ZAP-Queries](https://www.luogu.com.cn/problem/P3455)

## debug

开 `long long`。