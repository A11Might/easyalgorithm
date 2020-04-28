[861. 二分图的最大匹配](https://www.acwing.com/problem/content/863/)

#### 算法：

*#匈牙利算法*

#### 时间复杂度分析：



#### 代码：

```java
import java.util.*;

class Main {
    static final int N = 510, M = 100010;
    static int n1, n2, m;
    static int idx;
    static int[] h = new int[N], e = new int[M], ne = new int[M];
    static int[] match = new int[N];
    static boolean[] st = new boolean[N];

    static boolean find(int u) {
        for (int i = h[u]; i != -1; i = ne[i]) {
            int j = e[i];
            if (!st[j]) {
                st[j] = true;
                if (match[j] == 0 || find(match[j])) {
                    match[j] = u;
                    return true;
                }
            }
        }
        return false;
    }

    static void add(int u, int v) {
        e[idx] = v;
        ne[idx] = h[u];
        h[u] = idx++;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        n1 = sc.nextInt();
        n2 = sc.nextInt();
        m = sc.nextInt();

        Arrays.fill(h, -1);
        while (m-- > 0) {
            int u = sc.nextInt(), v = sc.nextInt();
            add(u, v);
        }

        int ret = 0;
        for (int i = 1; i <= n1; i++) {
            Arrays.fill(st, false);
            if (find(i)) ret++;
        }
        System.out.println(ret);
    }
}
```

