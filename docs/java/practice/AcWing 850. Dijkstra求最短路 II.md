[850. Dijkstra求最短路 II](https://www.acwing.com/problem/content/852/)

#### 算法：

*#dijkstra*

#### 时间复杂度分析：



#### 代码：

```java
import java.util.*;

class Main {
    static final int N = 150010, INF = 0x3f3f3f3f;
    static int n, m;
    static int h[] = new int[N], e[] = new int[N], ne[] = new int[N], w[] = new int[N], idx;
    static int[] dist = new int[N];
    static boolean[] st = new boolean[N];

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        n = sc.nextInt();
        m = sc.nextInt();

        Arrays.fill(h, -1);
        while (m-- > 0) {
            int a = sc.nextInt(), b = sc.nextInt(), c = sc.nextInt();
            add(a, b, c);
        }

        System.out.println(dijkstra());
    }

    static void add(int a, int b, int c) {
        e[idx] = b;
        w[idx] = c;
        ne[idx] = h[a];
        h[a] = idx++;
    }

    static int dijkstra() {
        Arrays.fill(dist, INF);
        dist[1] = 0;

        PriorityQueue<int[]> pq = new PriorityQueue<>((o1, o2) -> o1[0] - o2[0]); // [distance, index]
        pq.offer(new int[] {0, 1});
        while (!pq.isEmpty()) {
            var p = pq.poll();
            int u = p[1], d = p[0];

            if (st[u]) continue; // 当前点是冗余数据
            st[u] = true;

            for (int i = h[u]; i != -1; i = ne[i]) {
                int j = e[i];
                if (dist[j] > d + w[i]) {
                    dist[j] = d + w[i];
                    pq.offer(new int[] {dist[j], j});
                }
            }
        }

        if (dist[n] == INF) return -1;
        return dist[n];
    }
}
```

