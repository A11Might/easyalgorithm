[837. 连通块中点的数量](https://www.acwing.com/problem/content/839/)

#### 算法：

*#并查集*

#### 时间复杂度分析：



#### 代码：

```cpp
#include <bits/stdc++.h>

using namespace std;

const int N = 100010;

int p[N], cnt[N];

int find(int x) {
    if (p[x] != x) p[x] = find(p[x]);
    return p[x];
}

int main() {
    int n, m;
    cin >> n >> m;
    
    for (int i = 1; i <= n; i++) {
        p[i] = i;
        cnt[i] = 1;
    }
    
    while (m--) {
        string op;
        int a, b;
        cin >> op;
        
        if (op == "Q2") {
            cin >> a;
            cout << cnt[find(a)] << endl;
        } else {
            cin >> a >> b;
            a = find(a), b = find(b);
            if (op == "C") {
                // 当 a 和 b 在同一个连通块中则不能再连边
                // 否则会使连通块中元素个数翻倍
                if (a != b) {
                    cnt[b] += cnt[a];
                    p[a] = b;
                }
            } else {
                if (a == b) puts("Yes");
                else puts("No");
            }
        }
    }
    
    return 0;
}
```

