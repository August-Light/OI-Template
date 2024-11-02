# FFT & NTT

## 代码

时间复杂度 $\Theta(n \log n)$。

```cpp
void FFT(Complex a[], int n) {
    for (int i = 0; i < n; i++)
        if (rev[i] > i)
            swap(a[i], a[rev[i]]);
    for (int len = 2, m = 1; len <= n; len <<= 1, m <<= 1) {
        auto W = Complex(cos(PI / m), sin(PI / m));
        for (int l = 0, r = len-1; r < n; l += len, r += len) {
            auto w = Complex(1, 0);
            for (int i = l; i < l + m; i++) {
                auto x = a[i] + w * a[i + m], y = a[i] - w * a[i + m];
                a[i] = x, a[i + m] = y;
                w = w * W;
            }
        }
    }
}
void IFFT(Complex a[], int n) {
    FFT(a, n);
    reverse(a+1, a+n);
    for (int i = 0; i < n; i++)
        a[i] = a[i].real() / n;
}
```

```cpp
void NTT(ll a[], int n) {
    for (int i = 0; i < n; i++)
        if (rev[i] > i)
            swap(a[i], a[rev[i]]);
    for (int len = 2, m = 1; len <= n; len <<= 1, m <<= 1) {
        ll W = qpow(g, (MOD - 1) / len);
        for (int l = 0, r = len-1; r < n; l += len, r += len) {
            ll w = 1;
            for (int i = l; i < l + m; i++) {
                auto x = a[i] + w * a[i + m], y = a[i] - w * a[i + m];
                a[i] = x % MOD, a[i + m] = (y % MOD + MOD) % MOD;
                w = w * W % MOD;
            }
        }
    }
}
void INTT(ll a[], int n) {
    NTT(a, n);
    reverse(a+1, a+n);
    ll invn = inv(n);
    for (int i = 0; i < n; i++)
        a[i] = a[i] * invn % MOD;
}
```

```cpp
int rev[MAXN];

    int sum = n + m, tot = 1; while (tot <= sum) tot <<= 1;
    for (int i = 0; i < tot; i++)
        rev[i] = (rev[i >> 1] >> 1) | ((i & 1) << (__lg(tot) - 1));
```

## 注

手写复数：

```cpp
struct Complex {
    double re, im;
    Complex(double re = 0, double im = 0) : re(re), im(im) {}
    double real() {
        return re;
    }
    friend Complex operator+(Complex a, Complex b) {
        return Complex(a.re + b.re, a.im + b.im);
    }
    friend Complex operator-(Complex a, Complex b) {
        return Complex(a.re - b.re, a.im - b.im);
    }
    friend Complex operator*(Complex a, Complex b) {
        return Complex(a.re * b.re - a.im * b.im, a.re * b.im + a.im * b.re);
    }
};
```

高精度乘法最后的输出：

```cpp
    for (int i = 0; i <= sum; i++)
        ans[i] = c[i].real() + 0.5;
    int lim = sum;
    for (int i = 0; i <= lim; i++) {
        ans[i+1] += ans[i] / 10;
        ans[i] %= 10;
        if (i == lim && ans[i+1] != 0)
            lim++;
    }
    for (int i = lim; i >= 0; i--)
        cout << ans[i];
```

## 模板题目

[P3803 【模板】多项式乘法（FFT）](https://www.luogu.com.cn/problem/P3803)

[P1919 【模板】高精度乘法 | A*B Problem 升级版](https://www.luogu.com.cn/problem/P1919)