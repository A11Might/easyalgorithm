[848. 有向图的拓扑序列](https://www.acwing.com/problem/content/850/)

#### 算法：

*#拓扑排序*

#### 时间复杂度分析：

时间复杂度 O(n + m)，n 表示点数，m 表示边数。

#### 代码：

```java
import java.util.*;

class Main {
    static final int N = 100010, M = 2 * N;
    static int n, m, idx;
    static int[] h = new int [N], e = new int[N], ne = new int[N];
    static int[] q = new int[N], d = new int[N]; // 数组 d 记录每个节点的入度
    
    static void add(int x, int y) {
        e[idx] = y;
        ne[idx] = h[x];
        h[x] = idx++;
    }
    
    static boolean topoSort() {
        int hh = 0, tt = -1;
        
        for (int i = 1; i <= n; i++) {
            if (d[i] == 0) q[++tt] = i;
        }
        
        while (tt >= hh) {
            int u = q[hh++];
            for (int i = h[u]; i != -1; i = ne[i]) {
                int j = e[i];
                d[j]--;
                if (d[j] == 0) q[++tt] = j;
            }
        }
        
        return tt == n - 1;
    }
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        n = sc.nextInt();
        m = sc.nextInt();
        
        Arrays.fill(h, -1);
        for (int i = 0; i < m; i++) {
            int x = sc.nextInt(), y = sc.nextInt();
            add(x, y);
            d[y]++;
        }
        
        if (topoSort()) {
            for (int i = 0; i < n; i++) System.out.print(q[i] + " ");
        } else {
            System.out.println(-1);
        }
    }
}
```

