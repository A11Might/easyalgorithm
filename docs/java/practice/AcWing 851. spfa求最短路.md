[851. spfa求最短路](https://www.acwing.com/problem/content/853/)

#### 算法：

*#spfa*

#### 时间复杂度分析：



#### 代码：

```java
import java.util.*;

class Main {
    static final int N = 100010, INF = 0x3f3f3f3f;
    static int n, m;
    static int h[] = new int[N], w[] = new int[N], e[] = new int[N], ne[] = new int[N], idx;
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

        int ret = spfa();
        if (ret == INF) System.out.println("impossible");
        else System.out.println(ret);
    }

    static void add(int a, int b, int c) {
        e[idx] = b;
        w[idx] = c;
        ne[idx] = h[a];
        h[a] = idx++;
    }

    static int spfa() {
        Arrays.fill(dist, INF);
        dist[1] = 0;

        Queue<Integer> q = new ArrayDeque<>();
        q.offer(1);
        st[1] = true;
        
        while (!q.isEmpty()) {
            var u = q.poll();
            st[u] = false;

            for (int i = h[u]; i != -1; i = ne[i]) {
                int j = e[i];
                if (dist[j] > dist[u] + w[i]) {
                    dist[j] = dist[u] + w[i];
                    if (!st[j]) q.offer(j);
                }
            }
        }

        if (dist[n] == INF) return INF;
        return dist[n];
    }
}
```

