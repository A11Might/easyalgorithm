[853. 有边数限制的最短路](https://www.acwing.com/problem/content/855/)

#### 算法：

*#bellman - ford*

#### 时间复杂度分析：



#### 代码：

```java
import java.util.*;

class Edge {
    int a, b, w;

    Edge(int a, int b, int w) {
        this.a = a;
        this.b = b;
        this.w = w;
    }
}

class Main {
    static final int N = 510, M = 10010;
    static int n, m, k;
    static int[] dist = new int[N];
    // 使用 Bellman-Ford 算法可以随意存边，只要能遍历所有边即可
    static Edge[] edge = new Edge[M];

    static int bellmanFord() {
        Arrays.fill(dist, 0x3f3f3f3f);
        dist[1] = 0;

        for (int i = 0; i < k; i++) {
            // 备份 dist 数组，当前循环中的更新操作使用上次更新的结果，防止串连
            int[] backup = Arrays.copyOf(dist, N);
            for (int j = 0; j < m; j++) {
                int a = edge[j].a, b = edge[j].b, w = edge[j].w;
                if (dist[b] > backup[a] + w) {
                    dist[b] = backup[a] + w;
                }
            }
        }

        // 负权边可能会更新 0x3f3f3f3f 的值
        if (dist[n] > 0x3f3f3f3f / 2) return -1;
        return dist[n];
    }

    public static void main(String[] argsd) {
        Scanner sc = new Scanner(System.in);
        n = sc.nextInt();
        m = sc.nextInt();
        k = sc.nextInt();

        for (int i = 0; i < m; i++) {
            int a = sc.nextInt(), b = sc.nextInt(), w = sc.nextInt();
            edge[i] = new Edge(a, b, w);
        }

        int ret = bellmanFord();
        if(ret ==-1)System.out.println("impossible");
        else System.out.println(ret);
    }
}
```

