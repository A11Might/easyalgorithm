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

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        n = sc.nextInt();
        m = sc.nextInt();

        for (var col : g) Arrays.fill(col, INF);
        while (m-- > 0) {
            int a = sc.nextInt(), b = sc.nextInt(), w = sc.nextInt();
            g[a][b] = g[b][a] = Math.min(g[a][b], w); // 去重边
        }

        int ret = prim();
        if (ret == INF) System.out.println("impossible");
        else System.out.println(ret);
    }

    static int prim() {
        Arrays.fill(dist, INF);

        int ret = 0;
        for (int i = 0; i < n; i++) {
            int t = -1;
            for (int j = 1; j <= n; j++) {
                if (!st[j] && (t == -1 || dist[t] > dist[j])) t = j;
            }

            if (i != 0 && dist[t] == INF) return INF;

            if (i != 0) ret += dist[t];
            st[t] = true;

            for (int j = 1; j <= n; j++) dist[j] = Math.min(dist[j], g[j][t]);
        }
        
        return ret;
    }
}
```

