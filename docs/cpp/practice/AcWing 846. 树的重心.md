[846. 树的重心](https://www.acwing.com/problem/content/848/)

#### 算法：

*#dfs*

使用 dfs 求解树的问题时会先递归计算每个子树，再使用子树的结果解决当前树的问题，这种操作可以简化我们的计算，所以使用 dfs。

**具体算法**

使用 dfs 遍历整个树，每次遍历删除当前遍历到的节点 a，这样节点 a 的每个子节点就是一个连通图，从父节点往上又是一个连通图。

- 其中子节点为根结点的子树的节点个数可以通过 dfs 返回得到。
- 父节点往上部分的节点个数可以通过树的节点总数减去以节点 a 为根结点的树的节点个数得到。

这样就可以得到将节点 a 删除后，剩余各个连通块中点数的最大值。取所有得到的最大值中的最小值，就是表示重心的所有的子树中最大的子树的结点数目。

#### 时间复杂度分析：

每个节点只会遍历一次，所以总的时间复杂度为 O(n + m)，其中 n 为树中的节点个数，m 为树中的边数。

#### 代码：

```cpp
#include <iostream>
#include <cstring>

using namespace std;

const int N = 100010, M = 2 * N;

int n;
int h[N], e[M], ne[M], idx;
bool st[N];
int ret = N;

void add(int a, int b) {
    e[idx] = b, ne[idx] = h[a], h[a] = idx++;
}

int dfs(int u) {
    st[u] = true;
    
    int sum = 1, ans = 0;
    for (int i = h[u]; ~i; i = ne[i]) {
        int j = e[i];
        if (st[j]) continue;
        int s = dfs(j);
        sum += s;
        ans = max(ans, s);
    }
    
    ans = max(ans, n - sum);
    ret = min(ret, ans);
    
    return sum;
}

int main() {
    cin >> n;
    memset(h, -1, sizeof h);
    for (int i = 0; i < n - 1; i++) {
        int a, b;
        cin >> a >> b;
        add(a, b), add(b, a);
    }
    
    dfs(1);
    cout << ret << endl;
    
    return 0;
}
```

