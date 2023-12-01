# Floyd

## 代码

时间复杂度 $\Theta(n^3)$。

空间复杂度 $\Theta(n^2)$。

```cpp
ll dis[MAXN][MAXN];
void Floyd() {
    for (int k = 1; k <= n; k++)
        for (int i = 1; i <= n; i++)
            for (int j = 1; j <= n; j++)
                dis[i][j] = min(dis[i][j], dis[i][k] + dis[k][j]);
}
```

## 注

在 Floyd 前需要先把 `dis` 初始化为 $+\infty$。

## 模板题目

[B3647 【模板】Floyd](https://www.luogu.com.cn/problem/B3647)