[826. 单链表](https://www.acwing.com/problem/content/828/)

#### 算法：

*#单链表*

#### 时间复杂度分析：



#### 代码：

```cpp
#include <bits/stdc++.h>

using namespace std;

const int N = 100010;

int head, e[N], ne[N], idx;

// 将 x 插到头结点
void add_to_head(int x) {
    e[idx] = x, ne[idx] = head, head = idx++;
}

// 将 x 插到下标是 k 的点后面
void add(int k, int x) {
    e[idx] = x, ne[idx] = ne[k], ne[k] = idx++;
}

// 将下标是 k 的点后面的点删掉
void remove(int k) {
    ne[k] = ne[ne[k]];
}

int main() {
    int m;
    cin >> m;
    head = -1;
    while (m--) {
        int k, x;
        char op;

        cin >> op;
        if (op == 'H') {
            cin >> x;
            add_to_head(x);
        } else if (op == 'D') {
            cin >> k;
            if (!k) head = ne[head];
            else remove(k - 1); // 特盘删除头结点
        } else {
            cin >> k >> x;
            add(k - 1, x);
        }
    }
    
    for (int i = head; ~i; i = ne[i]) printf("%d ", e[i]);
    
    return 0;
}
```

