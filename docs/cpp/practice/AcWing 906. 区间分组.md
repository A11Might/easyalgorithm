[906. 区间分组](https://www.acwing.com/problem/content/908/)

#### 算法：

*#贪心*

1. 将所有区间按左端点从小到大排序。
2. 从前往后处理每个区间：
   - 判断能否将其放入某个现有的组中，L[i] > Max_r：
     - 如果不存在这样的组，则开新组，然后再将其放进去。
     - 如果存在这样的组，则将其放入其中任意一组，并更新当前组的 Max_r。

**证明**

- 如上算法过程可以保证每组中的区间都不相交，所以总组数 cnt 是一个可行解。假设最优解（最小组数）是 ans，可得 ans <= cnt。
- ans >= cnt
  - 第 cnt 组中存在区间 a 和前 cnt - 1 组中都有交集（不然的话区间 a 就可以放入到前 cnt - 1 组中了）也就是 L[cnt] < Max_r[cnt - 1]。
  - 因为是按照左端点从小到大排序，所以前 cnt - 1 组中所有区间的左端点都是小于第 cnt 组中的区间的左端点，也就是 L[1 ~ cnt - 1] < L[cnt]。
  - 综上，L[1 ~ cnt - 1] < L[cnt] < Max_r[cnt - 1]。也就是存在 cnt - 1 个区间与 cnt 中的区间 a 相交，所以最少需要 cnt 个组来分别放置这 cnt 个相交的区间 ，可得 ans >= cnt。
- 可以推出 ans = cnt。

#### 时间复杂度分析：



#### 代码：

```cpp
#include <iostream>
#include <algorithm>
#include <queue>

using namespace std;

const int N = 100010;

int n;
struct Range {
    int l, r;
    bool operator< (const Range &t)const {
        return l < t.l;
    }
} range[N];

int main() {
    cin >> n;
    for (int i = 0; i < n; i++) cin >> range[i].l >> range[i].r;
    
    sort(range, range + n);
    priority_queue<int, vector<int>, greater<int>> heap; // 小根堆
    
    for (int i = 0; i < n; i++) {
        auto u = range[i];
        if (heap.empty() || heap.top() >= u.l) heap.push(u.r);
        else {
            heap.pop();
            heap.push(u.r);
        }
    }
    
    cout << heap.size() << endl;
    
    return 0;
}
```

