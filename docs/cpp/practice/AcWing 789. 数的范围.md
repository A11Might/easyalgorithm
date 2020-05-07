[789. 数的范围](https://www.acwing.com/problem/content/791/)

#### 算法：

*#二分搜索*

#### 时间复杂度分析：

每次判断都会将数据规模减少一半，所以最多判断 logn 次，时间复杂度为 O(logn)。

#### 代码：

```cpp
#include <bits/stdc++.h>

using namespace std;

const int N = 100010;

int q[N];

int main() {
    int n, m;
    cin >> n >> m;
    for (int i = 0; i < n; i++) scanf("%d", &q[i]);
    
    while (m--) {
        int x;
        scanf("%d", &x);
        int l = 0, r = n - 1;
        while (l < r) {
            int mid = l + r >> 1;
            if (q[mid] >= x) r = mid;
            else l = mid + 1;
        }
        if (q[l] != x) cout << "-1 -1" << endl;
        else {
            cout << l << ' ';
            
            int l = 0, r = n - 1;
            while (l < r) {
                int mid = l + r + 1 >> 1;
                if (q[mid] <= x) l = mid;
                else r = mid - 1;
            }
            cout << l << endl;
        }
    }
    
    return 0;
}
```

