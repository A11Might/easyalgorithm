[859. Kruskal算法求最小生成树](https://www.acwing.com/problem/content/861/)

#### 算法：

*#kruskal*

#### 时间复杂度分析：



#### 代码：

```java
import java.util.*;

class Main {
    static final int N = 100010, M = 2 * N;
    static int n, m;
    static Edge[] edges = new Edge[M];
    static int[] p = new int[N];

    static int kruskal() {
        Arrays.sort(edges, 0, m, (o1, o2) -> o1.w - o2.w);
        for (int i = 0; i < n; i++) p[i] = i;

        int ret = 0, cnt = 0;
        for (int i = 0; i < m; i++) {
            int u = edges[i].u, v = edges[i].v, w = edges[i].w;
            u = find(u);
            v = find(v);
            if (u != v) {
                p[u] = v;
                ret += w;
                cnt++;
            }
        }

        if (cnt < n - 1) return -1;
        else return ret;
    }

    static int find(int x) {
        if (p[x] != x) p[x] = find(p[x]);
        return p[x];
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        n = sc.nextInt();
        m = sc.nextInt();

        for (int i = 0; i < m; i++) {
            int u = sc.nextInt(), v = sc.nextInt(), w = sc.nextInt();
            edges[i] = new Edge(u, v, w);
        }

        int ret = kruskal();
        if (ret == -1) System.out.println("impossible");
        else System.out.println(ret);
    }
}

class Edge {
    int u, v, w;

    public Edge(int u, int v, int w) {
        this.u = u;
        this.v = v;
        this.w = w;
    }
}
```

