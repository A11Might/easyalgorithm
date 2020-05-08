[829. 模拟队列](https://www.acwing.com/problem/content/831/)

#### 算法：

*#队列*

#### 时间复杂度分析：



#### 代码：

```cpp
#include <bits/stdc++.h>

using namespace std;

const int N = 100010;

int q[N], hh, tt;

int main() {
    int m;
    cin >> m;
    hh = 0, tt = -1;
    while (m--) {
        string op;
        int x;
        cin >> op;
        if (op == "push") {
            cin >> x;
            q[++tt] = x;
        } else if (op == "pop") {
            hh++;
        } else if (op == "empty") {
            if (hh <= tt) cout << "NO" << endl;
            else cout << "YES" << endl;
        } else {
            cout << q[hh] << endl;
        }
    }
    
    return 0;
}
```

