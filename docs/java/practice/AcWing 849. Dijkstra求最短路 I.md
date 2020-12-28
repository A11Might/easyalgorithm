[849. Dijkstra求最短路 I](https://www.acwing.com/problem/content/851/)

#### 算法：

*#dijkstra*

题目给定的数据范围数据：1 ≤ 节点数 ≤ 500，1 ≤ 边数 ≤10<sup>51</sup>。表示的图是稠密图，所以使用朴素 Dijkstra 算法。

#### 时间复杂度分析：

时间复杂是 O(n<sup>2</sup> + m)，n 表示点数，m 表示边数。

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

        // 自环：边权为正，对最短路没有影响
        // 重边：只保留边权最小的一个重边
        for (var col : g) Arrays.fill(col, INF);
        while (m-- > 0) {
            int a = sc.nextInt(), b = sc.nextInt(), w = sc.nextInt();
            g[a][b] = Math.min(g[a][b], w);
        }

        System.out.println(dijkstra());
    }

    static int dijkstra() {
        Arrays.fill(dist, INF);
        dist[1] = 0;

        for (int i = 0; i < n - 1; i++) {
            int t = -1;
            for (int j = 1; j <= n; j++) {
                if (!st[j] && (t == -1 || dist[t] > dist[j])) t = j;
            }
            st[t] = true;

            for (int j = 1; j <= n; j++) {
                // 边权等于 INF 时，表示没有边 t -> j
                // if (g[t][j] == INF) continue;
                dist[j] = Math.min(dist[j], dist[t] + g[t][j]);
            }
        }

        if (dist[n] == INF) return -1;
        return dist[n];
    }
}
```

