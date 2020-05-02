[905. 区间选点](https://www.acwing.com/problem/content/907/)

#### 算法：

*#贪心*

1. 将每个区间按右端点从小到大排序。
2. 从前往后依次枚举每个区间：
   - 如果当前区间已经包含点，则直接跳过。
   - 否则，选择当前区间的右端点（贪心，选择局部最优解来试图得到全局最优解）。

**证明**

- 如上算法，可以保证每个区间都包含一个点，是一个可行解记作 cnt。假设最优解（选择的点的最小数量）是 ans，可得 ans <= cnt。

- 算法过程中，如果当前区间已经包含点，则直接跳过。所以 cnt 个点，分别对应 cnt 个不相交的区间，但还有若干相交的区间，所以最优解 ans >= cnt。
- 可以推出 ans = cnt。

#### 时间复杂度分析：



#### 代码：

```cpp
#include <iostream>
#include <algorithm>

using namespace std;

const int N = 100010;

int n;
struct Range {
    int l, r;
    bool operator< (const Range &t)const {
        return r < t.r;
    }
} range[N];

int main() {
    cin >> n;
    for (int i = 0; i < n; i++) cin >> range[i].l >> range[i].r;
    sort(range, range + n);
    
    int ret = 0, ed = -2e9;
    for (int i = 0; i < n; i++) {
        if (range[i].l > ed) {
            ret++;
            ed = range[i].r;
        }
    }
    
    cout << ret << endl;
    
    return 0;
}
```

