# ST 表

## 代码

时间复杂度 $\Theta(n \log n) - \Theta(1)$。

空间复杂度 $\Theta(n \log n)$。

```cpp
struct ST {
    int f[LOGN][MAXN];
    void init() {
        rep(i, 1, n)
            f[0][i] = a[i];
        for (int i = 1; (1 << i) <= n; i++)
            for (int j = 1; j + (1 << i) - 1 <= n; j++)
                f[i][j] = max(f[i-1][j], f[i-1][j + (1 << (i-1))]);
    }
    int query(int l, int r) {
        int i = __lg(r - l + 1);
        return max(f[i][l], f[i][r - (1 << i) + 1]);
    }
};
```

## 注

这份代码支持静态区间查 $\max$。

## 模板题目

[P3865 【模板】ST 表](https://www.luogu.com.cn/problem/P3865)

## debug

- `+1` 和 `-1` 都写对了吗？