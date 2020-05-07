[802. 区间和](https://www.acwing.com/problem/content/804/)

#### 算法：

*#离散化*

操作和询问的坐标都是 10<sup>9</sup> 级别的，但操作数量只有 10<sup>5</sup> 级别。

我们求前缀和时，需要将坐标值当做下标来做，比如求坐标 [l, r] 之间的所有数字和，这样就需要开一个 10<sup>9</sup> 大小的数组，但数组并不能开出这么大，所以就可以使用离散化。

将所有需要用到的坐标放入数组中，排序、去重后离散化成从 1 开始的数，然后求前缀和。

#### 时间复杂度分析：



#### 代码：

```cpp
#include <bits/stdc++.h>

using namespace std;

typedef pair<int, int> PII;

const int N = 300010;

int n, m;
int a[N], s[N];
vector<int> alls;
vector<PII> add, query;

int find(int x) {
    int l = 0, r = alls.size() - 1;
    while (l < r) {
        int mid = l + r >> 1;
        if (alls[mid] >= x) r = mid;
        else l = mid + 1;
    }
    return r + 1;
}

int main() {
    cin >> n >> m;
    while (n--) {
        int x, c;
        scanf("%d%d", &x, &c);
        add.push_back({x, c});
        alls.push_back(x);
    }
    while (m--) {
        int l, r;
        scanf("%d%d", &l, &r);
        query.push_back({l, r});
        alls.push_back(l);
        alls.push_back(r);
    }
    
    // 去重
    sort(alls.begin(), alls.end());
    alls.erase(unique(alls.begin(), alls.end()), alls.end());
    
    // 处理插入
    for (auto item : add) {
        int x = find(item.first);
        a[x] += item.second;
    }
    
    // 预处理前缀和
    for (int i = 1; i <= alls.size(); i++) s[i] = s[i - 1] + a[i];
    
    // 处理查询
    for (auto item : query) {
        int l = find(item.first), r = find(item.second);
        printf("%d\n", s[r] - s[l - 1]);
    }
    
    return 0;
}
```

