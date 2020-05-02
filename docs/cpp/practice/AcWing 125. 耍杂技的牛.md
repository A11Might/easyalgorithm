[125. 耍杂技的牛](https://www.acwing.com/problem/content/127/)

#### 算法：

*#贪心*

按照 w<sub>i</sub> + s<sub>i</sub> 从小到大的顺序排列，最大的危险系数一定是最小的。

**证明**

假设最优解不是按照 w<sub>i</sub> + s<sub>i</sub> 从小到大的顺序排列，那么一定存在 w<sub>i</sub> + s<sub>i</sub> > w<sub>i + 1</sub> + s<sub>i + 1</sub>，我们交换这两头牛的位置。

因为牛的危险系数是：w<sub>1</sub> + w<sub>2</sub> + ... + w<sub>i</sub> - s<sub>i + 1</sub>，所以交换对其他牛的危险系数没有影响，我们只用考虑交换的两头牛。

|               | 交换前                                                       | 交换后                                                       |
| ------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 第 i 头牛     | w<sub>1</sub> + w<sub>2</sub> + ... + w<sub>i - 1</sub> - s<sub>i</sub> | w<sub>1</sub> + w<sub>2</sub> + ... + w<sub>i - 1</sub> - s<sub>i + 1</sub> |
| 第 i + 1 头牛 | w<sub>1</sub> + w<sub>2</sub> + ... + w<sub>i </sub> - s<sub>i + 1</sub> | w<sub>1</sub> + w<sub>2</sub> + ... + w<sub>i + 1</sub> - s<sub>i</sub> |

化简，同时减去 w<sub>1</sub> + w<sub>2</sub> + ... + w<sub>i - 1</sub>
|               | 交换前                             | 交换后                            |
| ------------- | ---------------------------------- | --------------------------------- |
| 第 i 头牛     | - s<sub>i</sub>                    | - s<sub>i + 1</sub>               |
| 第 i + 1 头牛 | w<sub>i </sub> - s<sub>i + 1</sub> | w<sub>i + 1</sub> - s<sub>i</sub> |

因为每个 w 和 s 都是大于等于 1 的，所以   w<sub>i </sub> - s<sub>i + 1</sub> > - s<sub>i + 1</sub>，同时 w<sub>i </sub> - s<sub>i + 1</sub> > w<sub>i + 1</sub> - s<sub>i</sub>，可以得到交换前危险值的最大值时大于交换后的，矛盾，假设不成立。

#### 时间复杂度分析：



#### 代码：

```cpp
#include <iostream>
#include <algorithm>

using namespace std;

typedef pair<int, int> PII;

const int N = 50010;

int n;
PII h[N];

int main() {
    cin >> n;
    for (int i = 0; i < n; i++) {
        int w, s;
        cin >> w >> s;
        h[i] = {w + s, s};
    }
    
    sort(h, h + n);
    
    int ret = -2e9, sum = 0;
    for (int i = 0; i < n; i++) {
        int w = h[i].first - h[i].second, s = h[i].second;
        ret = max(ret, sum - s);
        sum += w;
    }
    
    cout << ret << endl;
    return 0;
}
```

