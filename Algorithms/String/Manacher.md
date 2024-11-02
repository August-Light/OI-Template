# Manacher

## 代码

```cpp
int p[MAXN];
void manacher() {
    int n = S.length() - 1;
    int mid = 0, mx = 0;
    rep(i, 1, n) {
        if (i <= mx)
            p[i] = min(p[mid * 2 - i], mx - i);
        else
            p[i] = 1;
        while (i - p[i] >= 1 && i + p[i] <= n && S[i - p[i]] == S[i + p[i]])
            p[i]++;
        if (i + p[i] > mx)
            mx = i + p[i], mid = i;
    }
}
```

## 注

```cpp
int main() { ios::sync_with_stdio(0); cin.tie(0);
    cin >> S;
    n = S.length();
    string T = "~#";
    for (auto c : S)
        T.push_back(c), T.push_back('#');
    S = T;

    manacher();
    int m = S.length() - 1;
    int ans = 0;
    rep(i, 1, m)
        ans = max(ans, p[i] - 1);
    cout << ans << '\n';
    return 0;
}
```

## 模板题目

[P3805 【模板】manacher](https://www.luogu.com.cn/problem/P3805)

## debug

如果添加了分隔符号，要开两倍数组。