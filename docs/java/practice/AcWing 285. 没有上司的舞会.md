[285. 没有上司的舞会](https://www.acwing.com/problem/content/287/)

#### 算法：

*#DP#树形DP*

**状态表示 - f(u, 0) 和 f(u, 1)**

- 集合

  - f(u, 0) 表示所有从以 u 为根的子树中选，且不选 u 的方案。
  
  - f(u, 1) 表示所有从以 u 为根的子树中选，且选 u 的方案。

- 属性：Max

**状态计算**

按照当前节点 u 是否选择来分情况讨论：

- 选当前节点 u：如果选择节点 u，则 u 的所有子节点不能选择：f(u, 1) = w[u] + ∑f(s<sub>i</sub>, 0)。

- 不选当前节点 u：如果不选择节点 u，则 u 的子节点可以选择也可以不选择，取其中的最大值：f(u, 0) = ∑max(f(s<sub>i</sub>, 0), f(s<sub>i</sub>, 1))。

综上：ret = max(f(root, 0), f(root, 1))。

#### 时间复杂度分析：

一共有 2n 个状态，每个状态计算的时候会遍历它的所有儿子，每个状态的儿子加起来的总和应该等于树中边的数量 n - 1，所以总的时间复杂度是 O(n)。

#### 代码：

```java
import java.util.*;

class Main {
    static final int N = 6010;
    static int n;
    static int h[] = new int[N], e[] = new int[N], ne[] = new int[N], idx;
    static int[] happy = new int[N];
    static int[][] f = new int[N][2];
    static boolean[] hasFather = new boolean[N]; // 求树的根节点
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        n = sc.nextInt();
        for (int i = 1; i <= n; i++) happy[i] = sc.nextInt();
        
        Arrays.fill(h, -1);
        for (int i = 0; i < n - 1; i++) {
            int a = sc.nextInt(), b = sc.nextInt();
            add(b, a);
            hasFather[a] = true;
        }
        
        int root = 1;
        while (hasFather[root]) root++;
        
        dfs(root);
        
        int ret = Math.max(f[root][0], f[root][1]);
        System.out.println(ret);
    }
    
    static void add(int a, int b) {
        e[idx] = b;
        ne[idx] = h[a];
        h[a] = idx++;
    }
    
    static void dfs(int u) {
        f[u][1] = happy[u];
        
        for (int i = h[u]; i != -1; i = ne[i]) {
            int j = e[i];
            dfs(j);
    
            f[u][1] += f[j][0];
            f[u][0] += Math.max(f[j][0], f[j][1]);
        }
    }
}
```

