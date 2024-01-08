# 斐波那契循环节

## 代码

时间复杂度 $\Theta(\sqrt M)$。

```cpp
#include <bits/stdc++.h>
#define umap unordered_map
using namespace std;
typedef long long ll;
typedef unsigned long long ull;

string S;
ll MOD;

const int L = 2;
const ull BASE = 13331;
struct Matrix {
    ll M[L+1][L+1];
    ll *operator[](int p) {
        return M[p];
    }
    void clear() {
        memset(M, 0, sizeof M);
    }
    void reset() {
        clear();
        for (int i = 1; i <= L; i++)
            M[i][i] = 1;
    }
    Matrix friend operator*(Matrix A, Matrix B) {
        Matrix C; C.clear();
        for (int i = 1; i <= L; i++)
            for (int k = 1; k <= L; k++)
                for (int j = 1; j <= L; j++)
                    (C[i][j] += A[i][k] * B[k][j] % MOD) %= MOD;
        return C;
    }
    ull hs() {
        ull ret = 0;
        for (int i = 1; i <= L; i++)
            for (int j = 1; j <= L; j++)
                ret = ret * BASE + M[i][j];
        return ret;
    }

};
Matrix qpow(Matrix A, ll b) {
    Matrix Ret; Ret.reset();
    while (b) {
        if (b & 1)
            Ret = Ret * A;
        A = A * A;
        b >>= 1;
    }
    return Ret;
}

ll BSGS(Matrix A, Matrix B) {
    umap<ull, ll> mp;
    ll t = sqrt(MOD * 6) + 1;
    Matrix Cur; Cur.reset();
    for (ll i = 1; i <= t; i++) {
        mp[(Cur * B).hs()] = i-1;
        Cur = A * Cur;
    }
    Matrix Cur2 = Cur;
    for (ll i = 1; i <= t; i++) {
        if (mp.find(Cur2.hs()) != mp.end())
            return i * t - mp[Cur2.hs()];
        Cur2 = Cur * Cur2;
    }
    return -1;
}

Matrix A, I;
void init() {
    A[1][1] = 1; A[1][2] = 1;
    A[2][1] = 1; A[2][2] = 0;

    I[1][1] = 1; I[1][2] = 0;
    I[2][1] = 0; I[2][2] = 1;
}

ll fib(ll n) {
    if (n == 0)
        return 0;
    return qpow(A, n-1)[1][1];
}

int main() { ios::sync_with_stdio(0); cin.tie(0);
    cin >> S >> MOD;
    if (MOD == 1) {
        cout << 0 << endl;
        return 0;
    }
    init();
    ll pi = BSGS(A, I);
    ll n = 0;
    for (auto c : S)
        n = (n * 10 + (c - '0')) % pi;
    cout << fib(n) << endl;
    return 0;
}
```

## 注

此题是对矩阵做 BSGS。

这里的 `BSGS` 代码与普通 BSGS 不同，避开了 $0$ 这个解。

## 模板题目

[P4000 斐波那契数列](https://www.luogu.com.cn/problem/P4000)