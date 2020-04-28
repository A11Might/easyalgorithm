[858. Prim算法求最小生成树](https://www.acwing.com/problem/content/860/)

#### 算法：

*#prim*

#### 时间复杂度分析：



#### 代码：

```java
import java.util.*;

class Main {
    static final int N = 510, M = 100010, INF = 0x3f3f3f3f;
    static int n, m;
    static int[][] g = new int[N][N];
    static int[] dist = new int[N];
    static boolean[] st = new boolean[N];

    static int prim() {
        Arrays.fill(dist, INF);

        int ret = 0;
        for (int i = 0; i < n; i++) {
            int t = -1;
            for (int j = 1; j <= n; j++) {
                if (!st[j] && (t == -1 || dist[j] < dist[t])) t = j;
            }

            if (i != 0 && dist[t] == INF) return INF;
            if (i != 0) ret += dist[t];
            st[t] = true;

            for (int j = 1; j <= n; j++) dist[j] = Math.min(dist[j], g[j][t]);
        }

        return ret;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        n = sc.nextInt();
        m = sc.nextInt();

        for (var arr : g) Arrays.fill(arr, INF);
        while (m-- > 0) {
            int u = sc.nextInt(), v = sc.nextInt(), w = sc.nextInt();
            g[u][v] = g[v][u] = Math.min(g[u][v], w);
        }

        int ret = prim();
        if (ret == 0x3f3f3f3f) System.out.println("impossible");
        else System.out.println(ret);

    }
}
```

