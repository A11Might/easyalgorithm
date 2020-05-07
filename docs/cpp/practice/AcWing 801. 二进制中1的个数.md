[801. 二进制中1的个数](https://www.acwing.com/problem/content/803/)

#### 算法：

*#位运算*

每次减去给定整数 x 二进制中的最后一位 1（lowbit(n) = n & -n），一共能减几次 x 二进制中就有几个 1。

#### 时间复杂度分析：



#### 代码：

```cpp
#include <bits/stdc++.h>

using namespace std;

int main() {
    int n;
    cin >> n;
    
    while (n--) {
        int x;
        scanf("%d", &x);
        
        int cnt = 0;
        while (x) {
            cnt++;
            x -= x & -x;
        }
        printf("%d ", cnt);
    }
    
    return 0;
}
```

