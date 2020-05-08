[836. 合并集合](https://www.acwing.com/problem/content/838/)

#### 算法：

*#并查集*

#### 时间复杂度分析：



#### 代码：

```cpp
#include <bits/stdc++.h>

using namespace std;

const int N = 100010;

int n, m;
int p[N];

int find(int x) {
    if (p[x] != x) p[x] = find(p[x]);
    return p[x];
}

int main() {
    cin >> n >> m;
    for (int i = 1; i <= n; i++) p[i] = i;
    while (m--) {
        char op;
        int a, b;
        cin >> op >> a >> b;
        a = find(a), b = find(b);
        if (op == 'M') p[a] = b;
        else {
            if (a == b) puts("Yes");
            else puts("No");
        }
    }
    
    return 0;
}
```

