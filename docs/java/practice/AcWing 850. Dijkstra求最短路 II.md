[850. Dijkstra求最短路 II](https://www.acwing.com/problem/content/852/)

#### 算法：

*#dijkstra*

#### 时间复杂度分析：



#### 代码：

```java
import java.util.*;

class Main{
    static final int N = 150010;
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

    static int dijk() {
        Arrays.fill(dist, 0x3f3f3f3f);
        dist[1] = 0;
        PriorityQueue<int[]> heap = new PriorityQueue<>((o1, o2) -> o1[0] - o2[0]);
        heap.add(new int[] {dist[1], 1});
        while (!heap.isEmpty()) {
            var t = heap.poll();

            int ver = t[1], distance = t[0];

            if (st[ver]) continue;
            st[ver] = true;

            for (int i = h[ver]; i != -1; i = ne[i]) {
                int j = e[i];
                if (dist[j] > distance + w[i]) {
                    dist[j] = distance + w[i];
                    heap.add(new int[] {dist[j], j});
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

        System.out.println(dijk());
    }
}
```

