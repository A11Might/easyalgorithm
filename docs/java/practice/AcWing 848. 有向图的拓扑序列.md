[848. 有向图的拓扑序列](https://www.acwing.com/problem/content/850/)

#### 算法：

*#拓扑排序*

#### 时间复杂度分析：

时间复杂度 O(n + m)，n 表示点数，m 表示边数。

#### 代码：

```java
import java.util.*;

class Main {
    static final int N = 100010;
    static int n, m;
    static int h[] = new int[N], e[] = new int[N], ne[] = new int[N], idx;
    static int[] q = new int[N], d = new int[N]; // 每个点的入度

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        n = sc.nextInt();
        m = sc.nextInt();

        Arrays.fill(h, -1);
        while (m-- > 0) {
            int a = sc.nextInt(), b = sc.nextInt();
            add(a, b);
            d[b]++;
        }

        if (topsort()) {
            for (int i = 0; i < n; i++) System.out.print(q[i] + " ");
        } else System.out.print("-1");
        System.out.println();
    }

    static void add(int a, int b) {
        e[idx] = b;
        ne[idx] = h[a];
        h[a] = idx++;
    }

    static boolean topsort() {
        int hh = 0, tt = -1; // 初始化队列

        for (int i = 1; i <= n; i++) {
            if (d[i] == 0) q[++tt] = i;
        }

        while (hh <= tt) {
            int u = q[hh++];

            for (int i = h[u]; i != -1; i = ne[i]) {
                int j = e[i];
                if (--d[j] == 0) q[++tt] = j;
            }
        }

        return tt == n - 1;
    }
}
```

