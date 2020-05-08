[828. 模拟栈](https://www.acwing.com/problem/content/830/)

#### 算法：

*#栈*

#### 时间复杂度分析：



#### 代码：

```cpp
#include <bits/stdc++.h>

using namespace std;

const int N = 100010;

int stk[N], tt;

int main() {
    int m;
    cin >> m;
    while (m--) {
        string op;
        int x;
        cin >> op;
        if (op == "push") {
            cin >> x;
            stk[++tt] = x;
        } else if (op == "pop") {
            tt--;
        } else if (op == "empty") {
            if (tt == 0) cout << "YES" << endl;
            else cout << "NO" << endl;
        } else {
            cout << stk[tt] << endl;
        }
    }
    
    return 0;
}
```

