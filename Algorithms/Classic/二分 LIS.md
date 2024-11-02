# 二分 LIS

## 代码

时间复杂度 $\Theta(n \log n)$。

```cpp
int f[MAXN], tp;
int LIS(int a[]) {
    fill(f+1, f+n+1, INF);
    for (int i = 1; i <= n; i++) {
        int pos = lower_bound(f+1, f+tp+1, a[i]) - f;
        f[pos] = a[i];
        tp = max(tp, pos);
    }
    return tp;
}
```

## 注

这份代码支持求最长**上升**子序列（LIS）。

如果要求最长**不降**子序列（LNDS），可以将 `lower_bound` 改为 `upper_bound`：

```cpp
int f[MAXN], tp;
int LNDS(int a[]) {
    fill(f+1, f+n+1, INF);
    for (int i = 1; i <= n; i++) {
        int pos = upper_bound(f+1, f+tp+1, a[i]) - f;
        f[pos] = a[i];
        tp = max(tp, pos);
    }
    return tp;
}
```

## 模板题目

[LIS](https://www.luogu.com.cn/problem/AT_chokudai_S001_h)