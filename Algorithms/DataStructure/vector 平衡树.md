# vector 平衡树

## 代码

时间复杂度单次操作 $O(n)$。

空间复杂度 $O(n)$。

```cpp
#include <bits/stdc++.h>
using namespace std;

vector<int> v;

int main() { ios::sync_with_stdio(0); cin.tie(0);
    int q; cin >> q; while (q--) {
        int op, x; cin >> op >> x;
        if (op == 1) v.insert(lower_bound(v.begin(), v.end(), x), x);
        if (op == 2) v.erase(lower_bound(v.begin(), v.end(), x));
        if (op == 3) cout << lower_bound(v.begin(), v.end(), x) - v.begin() + 1 << '\n';
        if (op == 4) cout << v[x-1] << '\n';
        if (op == 5) cout << *prev(lower_bound(v.begin(), v.end(), x)) << '\n';
        if (op == 6) cout << *upper_bound(v.begin(), v.end(), x) << '\n';
    }
    return 0;
}
```

## 注

时间复杂度是假的。但是骗分很好用。

## 模板题目

[P3369 【模板】普通平衡树](https://www.luogu.com.cn/problem/P3369)