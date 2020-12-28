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
    static Edge[] g = new Edge[M];
    static int[] p = new int[N];

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        n = sc.nextInt();
        m = sc.nextInt();

        for (int i = 0; i < m; i++) {
            int a = sc.nextInt(), b = sc.nextInt(), w = sc.nextInt();
            g[i] = new Edge(a, b, w);
        }

        int ret = kruskal();
        if (ret == -1) System.out.println("impossible");
        else System.out.println(ret);
    }

    static int kruskal() {
        Arrays.sort(g, 0, m, (o1, o2) -> o1.w - o2.w);

        for (int i = 1; i <= n; i++) p[i] = i;

        int ret = 0, cnt = 0;
        for (int i = 0; i < m; i++) {
            Edge e = g[i];
            int a = e.a, b = e.b, w = e.w;
            a = find(a);
            b = find(b);
            if (a != b) {
                p[a] = b;
                ret += w;
                cnt++;
            }
        }

        if (cnt < n - 1) return -1;
        return ret;
    }

    static int find(int x) {
        if (p[x] != x) p[x] = find(p[x]);
        return p[x];
    }
}

class Edge {
    int a, b, w;

    public Edge(int a, int b, int w) {
        this.a = a;
        this.b = b;
        this.w = w;
    }
}
```

