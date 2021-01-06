[875. 快速幂](https://www.acwing.com/problem/content/877/)

#### 算法：

*#快速幂*

#### 时间复杂度分析：



#### 代码：

```cpp
#include <bits/stdc++.h>

using namespace std;

typedef long long LL;

LL qmi(int m, int k, int p) {
    LL ret = 1 % p;
    while(k) {
        if (k & 1) ret = ret * m % p;
        m = (LL) m * m % p;
        k >>= 1;
    }
    return ret;
}

int main() {
    int n;
    scanf("%d", &n);
    while (n--) {
        int m, k, p;
        scanf("%d%d%d", &m, &k, &p);
        printf("%lld\n", qmi(m, k, p));
    }
    
    return 0;
}
```

