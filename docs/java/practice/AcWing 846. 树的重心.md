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

```java
import java.util.*;

class Main {
    static final int N = 100010, M = 2 * N;
    static int n, ret = N;
    // 因为是无向图，所有给定的边都需要建立两条方向不同的边。
    static int[] h = new int[N], e = new int[M], ne = new int[M], idx;
    static boolean[] st = new boolean[N];

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        n = sc.nextInt();

        Arrays.fill(h, -1);
        // 注意是 n - 1 行数据
        for (int i = 0; i < n - 1; i++) {
            int a = sc.nextInt(), b = sc.nextInt();
            // 无向图存储两条有向边
            add(a, b);
            add(b, a);
        }

        // 因为每条边都是无向边，所以以哪个点开始都是一样的
        dfs(1);
        System.out.println(ret);
    }
    
    static void add(int a, int b) {
        e[idx] = b;
        ne[idx] = h[a];
        h[a] = idx++;
    }

    // 返回以 u 为根的子树中点的数量
    static int dfs(int u) {
        st[u] = true;

        // sum 表示以 u 为根结点的子树中节点个数，ans 表示删除 u 后剩余各个连通块中节点数的最大值
        int sum = 1, ans = 0;
        for (int i = h[u]; i != -1; i = ne[i]) {
            int j = e[i];
            if (st[j]) continue;

            int s = dfs(j);
            sum += s;
            ans = Math.max(ans, s);
        }

        ans = Math.max(ans, n - sum);
        // 在所有 ans 中取最小值
        ret = Math.min(ret, ans);

        return sum;
    }
}
```

