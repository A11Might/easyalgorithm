[851. spfa求最短路](https://www.acwing.com/problem/content/853/)

#### 算法：

*#spfa*

#### 时间复杂度分析：



#### 代码：

```java
import java.util.*;

class Main {
    static final int N = 100010;
    static int n, m, idx;
    static int[] h = new int[N], w = new int[N], e = new int[N], ne = new int[N];
    static int[] dist = new int[N];
    static boolean[] st = new boolean[N];

    static void add(int x, int y, int z) {
        e[idx] = y;
        w[idx] = z;
        ne[idx] = h[x];
        h[x] = idx++;
    }

    static int spfa() {
        Arrays.fill(dist, 0x3f3f3f3f);

        Queue<Integer> q = new ArrayDeque<>();
        q.offer(1);
        dist[1] = 0;
        st[1] = true;

        while (!q.isEmpty()) {
            int t = q.poll();
            st[t] = false;

            for (int i = h[t]; i != -1; i = ne[i]) {
                int j = e[i];
                if (dist[j] > dist[t] + w[i]) {
                    dist[j] = dist[t] + w[i];
                    if (!st[j]) {
                        q.offer(j);
                        st[j] = true;
                    }
                } 
            }
        }

        if (dist[n] == 0x3f3f3f3f) return -1;
        return dist[n];
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        n = sc.nextInt();
        m = sc.nextInt();

        Arrays.fill(h, -1);
        while (m-- > 0) {
            int x = sc.nextInt(), y = sc.nextInt(), z = sc.nextInt();
            add(x, y, z);
        }

        int ret = spfa();
        if (ret == -1) System.out.println("impossible");
        else System.out.println(ret);
    }
}
```

