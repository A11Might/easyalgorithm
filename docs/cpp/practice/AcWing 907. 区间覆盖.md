[907. 区间覆盖](https://www.acwing.com/problem/content/909/)

#### 算法：

*#贪心*

1. 将区间按照左端点从小到大排序。
2. 从前往后依次枚举每个区间，在所有能覆盖 s 的区间中，选择右端点最大的区间，然后将 s 更新为该区间的右端点。

**证明**

假设如上算法得到的可行解的区间数是 cnt，最优解（最少区间数）是 ans。

我们寻找两组区间中第一个不同的区间 a, b：

- 这两个不同的区间 a，b 的左端点都与前一个区间（是相同的）相交。
- 如上算法得到的可行解的区间 a 的右端点是最大的，也就是说它一定大于最优解中对应的区间 b 的右端点。
- 综上，我们可以使用可行解中的区间 a 替换最优解中的区间 b，并且这个操作对方案中的区间数是没有影响的。

然后我们依次对其余不同的区间进行替换，最终可行解 cnt 和 最优解 ans 变得完全相同，可以得到 ans = cnt。

#### 时间复杂度分析：



#### 代码：

```cpp
#include <iostream>
#include <algorithm>

using namespace std;

const int N = 100010;

int n, s, t;
struct Range {
    int l, r;
    bool operator< (const Range &t)const {
        return l < t.l;
    }
} range[N];

int main() {
    cin >> s >> t >> n;
    for (int i = 0; i < n; i++) cin >> range[i].l >> range[i].r;
    
    sort(range, range + n);
    
    int ret = 0;
    for (int i = 0; i < n; i++) {
        int j = i, r = -2e9;
        while (j < n && range[j].l <= s) {
            r = max(r, range[j].r);
            j++;
        }
        
        // 没法覆盖
        if (r < s) {
            puts("-1");
            return 0;
        }
        
        ret++;
        s = r;
        i = j - 1;
        
        // 已经完全覆盖
        if (r >= t) {
            cout << ret << endl;
            return 0;
        }
    }
    
    // 没法完全覆盖
    puts("-1");
    
    return 0;
}
```

