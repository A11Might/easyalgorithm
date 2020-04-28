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
    static final int N = 510;
    static int n, m;
    static int[][] g = new int[N][N];
    static int[] dist = new int[N];
    static boolean[] st = new boolean[N];
    
    static int dijk() {
        Arrays.fill(dist, 0x3f3f3f3f);
        dist[1] = 0;
        
        for (int i = 0; i < n - 1; i++) {
            int t = -1;
            for (int j = 1; j <= n; j++) {
                if (!st[j] && (t == -1 || dist[j] < dist[t])) t = j;
            }
            
            for (int j = 1; j <= n; j++) {
                // 边权全部初始化为Integer.MAX_VALUE时
                // 边权等于 Integer.MAX_VALUE 时，表示没有边 t -> j
                // if (g[t][j] == Integer.MAX_VALUE) continue;
                dist[j] = Math.min(dist[j], dist[t] + g[t][j]);
            }
            
            st[t] = true;
        }
        
        if (dist[n] == 0x3f3f3f3f) return -1;
        return dist[n];
    }
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        n = sc.nextInt();
        m = sc.nextInt();
        
        // 自环：边权为正，对最短路没有影响
        // 重边：只保留边权最小的一个重边
        for (var arr : g) Arrays.fill(arr, 0x3f3f3f3f);
        for (int i = 0; i < m; i++) {
            int x = sc.nextInt(), y = sc.nextInt(), z = sc.nextInt();
            g[x][y] = Math.min(g[x][y], z);
        }
        
        System.out.println(dijk());
    }
}
```

