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
int b[N];

void insert(int l, int r, int x) {
    b[l] += x, b[r + 1] -= x;
}

int main() {
    scanf("%d%d", &n, &m);
    
    // 构建差分序列
    for (int i = 1; i <= n; i++) {
        int x;
        scanf("%d", &x);
        insert(i, i, x); 
    }
    
    // m 次区间加 c 操作
    while (m--) {
        int l, r, x;
        scanf("%d%d%d", &l, &r, &x);
        insert(l, r, x);
    }
    
    for (int i = 1; i <= n; i++) {
        b[i] = b[i - 1] + b[i]; // 求差分序列的前缀和
        printf("%d ", b[i]);
    }
    
    return 0;
}
```

