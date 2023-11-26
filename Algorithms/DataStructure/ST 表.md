# ST 表

## 代码

时间复杂度 $\Theta(n \log n) - \Theta(1)$。

空间复杂度 $\Theta(n \log n)$。

```cpp
struct ST {
    int f[MAXN][MAXT];
    void build() {
        for (int i = 1; i <= n; i++)
            f[i][0] = a[i];
        for (int j = 1; j <= 18; j++)
            for (int i = 1; i+(1<<j)-1 <= n; i++)
                f[i][j] = max(f[i][j-1], f[i+(1<<(j-1))][j-1]);
    }
    int query(int l, int r) {
        int j = __lg(r - l + 1);
        return max(f[l][j], f[r-(1<<j)+1][j]);
    }
};
```

## 注

这份代码支持静态区间查 $\max$。

## 模板题目

[P3865 【模板】ST 表](https://www.luogu.com.cn/problem/P3865)

## debug

- `+1` 和 `-1` 都写对了吗？