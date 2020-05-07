[795. 前缀和](https://www.acwing.com/problem/content/797/)

#### 算法：

*#前缀和*

#### 时间复杂度分析：

预处理前缀和需要遍历一遍数组，时间复杂度为 O(n)。

#### 代码：

```cpp
#include <bits/stdc++.h>

using namespace std;

const int N = 100010;

int n, m;
int a[N], s[N];

int main() {
    cin >> n >> m;
    for (int i = 1; i <= n; i++) scanf("%d", &a[i]);
    
    // 初始化前缀和
    for (int i = 1; i <= n; i++) s[i] = s[i - 1] + a[i];
    
    while (m--) {
        int l, r;
        scanf("%d%d", &l, &r);
        printf("%d\n", s[r] - s[l - 1]); // 计算区间和
    }
    
    return 0;
}
```

