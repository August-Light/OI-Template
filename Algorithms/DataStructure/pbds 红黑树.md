# pbds 红黑树

## 代码

时间复杂度单次操作 $O(\log n)$。

空间复杂度 $O(n)$。

```cpp
template<typename Val>
struct SBT {
    typedef pair<int, Val> pii;
    tree<pii, null_type, less<pii>, rb_tree_tag, tree_order_statistics_node_update> tr;
    int cnt = 0;
    void ins(Val k) {
        tr.insert({k, ++cnt});
    }
    void del(Val k) {
        tr.erase(tr.lower_bound({k, 0}));
    }
    int rnk(Val k) {
        return tr.order_of_key({k, 0}) + 1;
    }
    Val kth(int x) {
        return tr.find_by_order(x - 1)->first;
    }
    Val pre(Val k) {
        return kth(rnk(k) - 1);
    }
    Val nxt(Val k) {
        return kth(rnk(k + 1));
    }
};
```

## 注

需加上这两行：

```cpp
#include <bits/extc++.h>
using namespace __gnu_pbds;
```

考场上可能需要 `#include <ext/pb_ds/assoc_container.hpp>`。

## 模板题目

[P3369 【模板】普通平衡树](https://www.luogu.com.cn/problem/P3369) & [P6136 【模板】普通平衡树（数据加强版）](https://www.luogu.com.cn/problem/P6136)