[854. Floyd求最短路](https://www.acwing.com/problem/content/856/)

#### 算法：

*#floyd*

#### 时间复杂度分析：



#### 代码：

```java
import java.util.*;

class Main {
    static final int N = 210, M = 20010;
    static int n, m, k;
    static int[][] d = new int[N][N];

    static void floyd() {
        for (int k = 1; k <= n; k++) {
            for (int i = 1; i <= n; i++) {
                for (int j = 1; j <= n; j++) {
                    d[i][j] = Math.min(d[i][j], d[i][k] + d[k][j]);
                }
            }
        }
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        n = sc.nextInt();
        m = sc.nextInt();
        k = sc.nextInt();

        // 去掉重边和自环
        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= n; j++) {
                if (i == j) d[i][j] = 0;
                else d[i][j] = 0x3f3f3f3f;
            }
        }

        while (m-- > 0) {
            int x = sc.nextInt(), y = sc.nextInt(), z = sc.nextInt();
            d[x][y] = Math.min(d[x][y], z);
        }

        floyd();

        while (k-- > 0) {
            int x = sc.nextInt(), y = sc.nextInt();
            int ret = d[x][y];
            if (ret > 0x3f3f3f3f / 2) System.out.println("impossible");
            else System.out.println(ret);
        }
    }
}
```

