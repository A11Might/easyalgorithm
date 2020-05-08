[838. 堆排序](https://www.acwing.com/problem/content/840/)

#### 算法：

*#堆*

#### 时间复杂度分析：



#### 代码：

```cpp
#include <bits/stdc++.h>

using namespace std;

const int N = 100010;

int h[N], cnt;

// 向下堆化
void down(int u) {
    int t = u;
    if (u * 2 <= cnt && h[u * 2] < h[t]) t = u * 2;
    if (u * 2 + 1 <= cnt && h[u * 2 + 1] < h[t]) t = u * 2 + 1;
    if (u != t) {
        swap(h[u], h[t]);
        down(t);
    }
}

int main() {
    int n, m;
    cin >> n >> m;
    cnt = n;
    for (int i = 1; i <= n; i++) cin >> h[i];
    
    for (int i = n / 2; i; i--) down(i); // 建堆
    
    while (m--) {
        printf("%d ", h[1]);
        h[1] = h[cnt--];
        down(1);
    }
    puts("");
    
    return 0;
}
```

