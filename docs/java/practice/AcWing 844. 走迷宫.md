[844. 走迷宫](https://www.acwing.com/problem/content/846/)

#### 算法：

*#bfs*

**拓展 - 打印路径**

记录每个位置是从哪个位置走过来的，然后倒着往前推就行了。

#### 时间复杂度分析：



#### 代码：

数组模拟队列

```java
import java.util.*;

class Main {
    static final int N = 110;
    static int n, m, hh, tt;
    static int[][] g = new int[N][N], d = new int[N][N], q = new int[N * N][2];
    static int[][] direction = {{1, 0}, {-1, 0}, {0, 1}, {0, -1}};

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        n = sc.nextInt();
        m = sc.nextInt();
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                g[i][j] = sc.nextInt();
            }
        }

        for (var arr : d) Arrays.fill(arr, -1);
        hh = 0;
        tt = -1;
        d[0][0] = 0;
        q[++tt][0] = q[tt][1] = 0;
        while (tt >= hh) {
            int i = q[hh][0], j = q[hh++][1];
            for (var dir : direction) {
                int x = i + dir[0], y = j + dir[1];
                if (x < 0 || x >= n || y < 0 || y >= m || g[x][y] == 1 || d[x][y] != -1) continue;
                d[x][y] = d[i][j] + 1;
                q[++tt][0] = x;
                q[tt][1] = y;
            }
        }

        System.out.println(d[n - 1][m - 1]);
    }
}
```



打印路径

```java
import java.util.*;

class Main {
    static final int N = 110;
    static int n, m, hh, tt;
    static int[][] g = new int[N][N], d = new int[N][N], q = new int[N * N][2];
    static int[][][] pre = new int[N][N][2];
    static int[][] direction = {{1, 0}, {-1, 0}, {0, 1}, {0, -1}};

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        n = sc.nextInt();
        m = sc.nextInt();
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                g[i][j] = sc.nextInt();
            }
        }

        for (var arr : d) Arrays.fill(arr, -1);
        hh = 0;
        tt = -1;
        d[0][0] = 0;
        q[++tt][0] = q[tt][1] = 0;
        while (tt >= hh) {
            int i = q[hh][0], j = q[hh++][1];
            for (var dir : direction) {
                int x = i + dir[0], y = j + dir[1];
                if (x < 0 || x >= n || y < 0 || y >= m || g[x][y] == 1 || d[x][y] != -1) continue;
                pre[x][y][0] = i;
                pre[x][y][1] = j;
                d[x][y] = d[i][j] + 1;
                q[++tt][0] = x;
                q[tt][1] = y;
            }
        }

        int i = n - 1, j = m - 1;
        while (i != 0 || j != 0) {
            System.out.println(i + " " + j);
            var p = pre[i][j];
            i = p[0];
            j = p[1];
        }

        System.out.println(d[n - 1][m - 1]);
    }
}
```

