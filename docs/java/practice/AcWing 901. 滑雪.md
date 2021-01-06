[901. 滑雪](https://www.acwing.com/problem/content/903/)

#### 算法：

*#DP#记忆化搜索*

**状态表示 - f(i, j)**

- 集合：所有从 (i, j) 开始滑的路径

- 属性：Max

**状态计算 - 集合划分**

按照第一步滑的方向来划分 f(i, j) 表示的集合：

- 第一步向上滑

- 第一步向下滑

- 第一步向左滑

- 第一步向右滑：先从 (i, j) 滑到 (i, j + 1)，再从 (i, j + 1) 滑开始滑，当 h\[i][j] < h\[i][j + 1] 时这种情况不存在。

  我们可以先考虑从 (i, j + 1) 滑的路径的最大值，然后再加上从 (i, j) 到 (i, j + 1) 的路径：f(i, j + 1) + 1。

综上：将所有存在的情况求出取 max。

#### tips

使用递归求动态规划，需要保证存在拓扑序，也就是不存在路径 a -> b -> c -> a。

因为只有前一个位置比后一个位置高时才存在路径，如果上述路径存在，则 h[a] > h[a]，就矛盾了，所以不存在上述路径，可以使用递归。

#### 时间复杂度分析：



#### 代码：

```java
import java.util.*;

class Main {
    static final int N = 310;
    static int n, m;
    static int[][] h = new int[N][N];
    static int[][] f = new int[N][N];
    static int[] dx = {-1, 0, 1, 0}, dy = {0, 1, 0, -1};
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        n = sc.nextInt();
        m = sc.nextInt();
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                h[i][j] = sc.nextInt();
            }
        }
        
        // 初始时设每个状态都没访问过
        for (var arr : f) Arrays.fill(arr, -1); 
        
        int ret = 0;
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                ret = Math.max(ret, dp(i, j));
            }
        }
        
        System.out.println(ret);
    }
    
    static int dp(int i, int j) {
        if (f[i][j] != -1) return f[i][j];
        
        f[i][j] = 1;
        for (int k = 0; k < 4; k++) {
            int x = i + dx[k], y = j + dy[k];
            if (x < 0 || x >= n || y < 0 || y >= m || h[x][y] >= h[i][j]) continue;
            f[i][j] = Math.max(f[i][j], dp(x, y) + 1);
        }
        
        return f[i][j];
    }
}
```

