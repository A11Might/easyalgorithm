[860. 染色法判定二分图](https://www.acwing.com/problem/content/862/)

#### 算法：

*#染色法*

#### 时间复杂度分析：



#### 代码：

```java
import java.util.*;

class Main {
    static final int N = 100010, M = 2 * N;
    static int n, m;
    static int idx;
    static int[] h = new int[N], e = new int[M], ne = new int[M];
    static int[] color = new int[N];

    static boolean dfs(int u, int c) {
        color[u] = c;

        for (int i = h[u]; i != -1; i = ne[i]) {
            int j = e[i];
            if (color[j] == 0) {
                if (!dfs(j, 3 - c)) return false;
            } else if (color[j] == c) return false;
        }

        return true;
    }

    static void add(int u, int v) {
        e[idx] = v;
        ne[idx] = h[u];
        h[u] = idx++;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        n = sc.nextInt();
        m = sc.nextInt();

        Arrays.fill(h, -1);
        while (m-- > 0) {
            int u = sc.nextInt(), v = sc.nextInt();
            add(u, v);
            add(v, u);
        }

        boolean flag = true;
        for (int i = 1; i <= n; i++) {
            if (color[i] == 0) {
                if (!dfs(i, 1)) {
                    flag = false;
                    break;
                }
            }
        }

        if (flag) System.out.println("Yes");
        else System.out.println("No");
    }
}
```

