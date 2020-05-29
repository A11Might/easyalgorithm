[841. 字符串哈希](https://www.acwing.com/problem/content/843/)

#### 算法：

*#字符串哈希*

#### 时间复杂度分析：



#### 代码：

```cpp
#include <bits/stdc++.h>

#define ULL unsigned long long

using namespace std;

const int N = 100010, P = 131;

int n, m;
char str[N];
ULL h[N], p[N];

ULL get(int l, int r) {
    return h[r] - h[l - 1] * p[r - l + 1];
}

int main() {
    cin >> n >> m >> str + 1;
    
    p[0] = 1;
    for (int i = 1; i <= n; i++) {
        h[i] = h[i - 1] * P + str[i];
        p[i] = p[i - 1] * P; 
    }
    
    while (m--) {
        int l1, r1, l2, r2;
        cin >> l1 >> r1 >> l2 >> r2;
        if (get(l1, r1) == get(l2, r2)) puts("Yes");
        else puts("No");
    }
    
    return 0;
}
```

