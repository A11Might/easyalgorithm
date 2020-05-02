[908. 最大不相交区间数量](https://www.acwing.com/problem/content/910/)

#### 算法：

*#贪心*

1. 将每个区间按右端点从小到大排序。
2. 从前往后依次枚举每个区间：
   - 如果当前区间已经包含点，则直接跳过，不选这个区间。
   - 否则，就选择当前区间，并更新点为当前区间的右端点。

**证明**

- 算法过程中，如果当前区间已经包含点，则不选当前区间。也就是说选出的 cnt 个点，分别对应 cnt 个不相交的个区间，所以 cnt 是一个可行解，假设最优解（可选取区间的最大数量）是 ans，可得 ans >= cnt。

- ans <= cnt

  反证法：假设 ans > cnt，也就是说最多存在 ans 个不相交的区间，所以我们至少需要 ans 个点才能覆盖所有区间，但由【905. 区间选点】可知我们选出的 cnt 个点就可以覆盖所有区间，矛盾了，所以假设不成立，ans <= cnt。

- 可以推出，ans = cnt。

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

