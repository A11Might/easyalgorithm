[797. 差分](https://www.acwing.com/problem/content/799/)

#### 算法：

*#差分*

#### 时间复杂度分析：

插入操作的时间复杂度为 O(1)。

#### 代码：

```cpp
#include <bits/stdc++.h>

using namespace std;

const int N = 100010;

int n, m;
int a[N], b[N];

void insert(int l, int r, int c) {
    b[l] += c, b[r + 1] -= c;
}

int main() {
    cin >> n >> m;
    for (int i = 1; i <= n; i++) scanf("%d", &a[i]);
    for (int i = 1; i <= n; i++) insert(i, i, a[i]);  // 差分序列
    
    // m 次区间加 c 操作
    while (m--) {
        int l, r, c;
        scanf("%d%d%d", &l, &r, &c);
        insert(l, r, c);
    }
    
    for (int i = 1; i <= n; i++) b[i] += b[i - 1]; // 求 b 的前缀和 
    for (int i = 1; i <= n; i++) printf("%d ", b[i]);
    
    return 0;
}
```

