[893. 集合-Nim游戏](https://www.acwing.com/problem/content/895/)

#### 算法：

*SG函数*

![](4-3.png)

#### 时间复杂度分析：



#### 代码：

```cpp
#include <iostream>
#include <cstring>
#include <unordered_set>

using namespace std;

const int N = 110, M = 10010;

int k, n;
int s[N], f[M];

// 记忆化搜索
int sg(int x) {
    if (~f[x]) return f[x];
    
    // 计算 sg(y1), sg(y2), ...
    unordered_set<int> S;
    for (int i = 0; i < k; i++) {
        if (x >= s[i]) S.insert(sg(x - s[i]));
    }
    
    // mex 操作，计算 sg(x)
    for (int i = 0; ; i++) {
        if (!S.count(i)) return f[x] = i;
    }
}

int main() {
    cin >> k;
    for (int i = 0; i < k; i++) cin >> s[i];
    
    cin >> n;
    
    memset(f, -1, sizeof f);
    
    int ret = 0;
    while (n--) {
        int h;
        cin >> h;
        ret ^= sg(h);
    }
    
    if (ret) puts("Yes");
    else puts("No");
    
    return 0;
}
```

