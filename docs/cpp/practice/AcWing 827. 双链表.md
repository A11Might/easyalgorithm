[827. 双链表](https://www.acwing.com/problem/content/829/)

#### 算法：

*#双链表*

#### 时间复杂度分析：



#### 代码：

```cpp
#include <bits/stdc++.h>

using namespace std;

const int N = 100010;

int e[N], l[N], r[N], idx;

// 在节点 k 的右边插入一个数 x
void insert(int k, int x) {
    e[idx] = x;
    r[idx] = r[k], l[idx] = k;
    l[r[k]] = idx, r[k] = idx++;
}

// 删除节点 k
void remove(int k) {
    l[r[k]] = l[k];
    r[l[k]] = r[k];
}

int main() {
    int m;
    cin >> m;
    
    r[0] = 1, l[1] = 0;
    idx = 2;
    
    while (m--) {
        int k, x;
        string op;
        cin >> op;
        if (op == "L") {
            cin >> x;
            insert(0, x);
        } else if (op == "R") {
            cin >> x;
            insert(l[1], x);
        } else if (op == "D") {
            cin >> k;
            remove(k + 1);
        } else if (op == "IL") {
            cin >> k >> x;
            insert(l[k + 1], x);
        } else {
            cin >> k >> x;
            insert(k + 1, x);
        }
    }
    
    for (int i = r[0]; i != 1; i = r[i]) cout << e[i] << ' ';
    cout << endl;
    
    return 0;
}
```

