[852. spfa判断负环](https://www.acwing.com/problem/content/854/)

#### 算法：

*#spfa*

#### 时间复杂度分析：



#### 代码：

```java
import java.util.*;

class Main {
    static final int N = 2010, M = 10010;
    static int n, m;
    static int h[] = new int[N], w[] = new int[M], e[] = new int[M], ne[] = new int[M], idx;
    static int[] dist = new int[N], cnt = new int[N]; // cnt[x]存储 1 到 x 的最短路中经过的点数
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

        if (spfa()) System.out.println("Yes");
        else System.out.println("No");
    }

    static void add(int a, int b, int c) {
        e[idx] = b;
        w[idx] = c;
        ne[idx] = h[a];
        h[a] = idx++;
    }

    static boolean spfa() {
        Queue<Integer> q = new ArrayDeque<>();
        for (int i = 1; i <= n; i++) {
            q.offer(i);
            st[i] = true;
        }

        while (!q.isEmpty()) {
            var u = q.poll();
            st[u] = false;

            for (int i = h[u]; i != -1; i = ne[i]) {
                int j = e[i];
                if (dist[j] > dist[u] + w[i]) {
                    dist[j] = dist[u] + w[i];
                    cnt[j] = cnt[u] + 1;
                    // 如果从 1 号点到 x 的最短路中包含至少 n 个点（不包括自己），则说明存在环
                    if (cnt[j] >= n) return true;
                    if (!st[j]) q.offer(j);
                }
            }
        }

        return false;
    }
}
```

