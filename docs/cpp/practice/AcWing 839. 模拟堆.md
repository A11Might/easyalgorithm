[839. 模拟堆](https://www.acwing.com/problem/content/841/)

#### 算法：

*#堆*

#### 时间复杂度分析：



#### 代码：

```cpp
#include <bits/stdc++.h>

using namespace std;

const int N = 100010;

int h[N], cnt, hp[N], ph[N], idx;

void heap_swap(int a, int b) {
    swap(h[a], h[b]);
    swap(hp[a], hp[b]);
    swap(ph[hp[a]], ph[hp[b]]);
}

void down(int u) {
    int t = u;
    if (u * 2 <= cnt && h[u * 2] < h[t]) t = u * 2;
    if (u * 2 + 1 <= cnt && h[u * 2 + 1] < h[t]) t = u * 2 + 1;
    if (u != t) {
        heap_swap(u, t);
        down(t);
    }
}

void up(int u) {
    int t = u;
    while (u / 2 && h[u] < h[u / 2]) {
        heap_swap(u, u / 2);
        u >>= 1;
    }
}

int main() {
    int n;
    cin >> n;
    while (n--) {
        string op;
        int k, x;
        cin >> op;
        if (op == "I") {
            cin >> x;
            cnt++;
            idx++;
            ph[idx] = cnt, hp[cnt] = idx;
            h[cnt] = x;
            up(cnt);
        } else if (op == "PM") cout << h[1] << endl;
        else if (op == "DM") {
            heap_swap(1, cnt--);
            down(1);
        } else if (op == "D") {
            cin >> k;
            k = ph[k];
            heap_swap(k, cnt--);
            up(k), down(k);
        } else {
            cin >> k >> x;
            k = ph[k];
            h[k] = x;
            up(k), down(k);
        }
    }
    
    return 0;
}
```

