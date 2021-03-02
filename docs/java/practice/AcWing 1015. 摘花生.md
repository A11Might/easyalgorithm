[1015. 摘花生](https://www.acwing.com/problem/content/1017/)

#### 算法：

*DP* *数字三角形模型*

**状态表示 - f(i, j)**

- 集合：所有从 (1, 1) 走到 (i, j) 的路线

- 属性：Max

**状态计算 - 集合划分**

以最后一步来划分 f(i, j) 表示的集合：

- 最后一步是从上面下来的：f(i - 1, j) + w(i, j)

- 最后一步是从左边过来的：f(i, j - 1) + w(i, j)

综上：f(i, j) = max(f(i - 1, j), f(i, j - 1)) + w(i, j)。

#### 时间复杂度分析：



#### 代码：

```java
import java.util.*;

class Main {
	static final int N = 110;
	static int n, m;
	static int[][] w = new int[N][N];
	static int[][] f = new int[N][N];

	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		int T = sc.nextInt();
		while (T-- > 0) {
			n = sc.nextInt();
			m = sc.nextInt();
			for (int i = 1; i <= n; i++) {
				for (int j = 1; j <= m; j++) {
					w[i][j] = sc.nextInt();
				}
			}

			for (int i = 1; i <= n; i++) {
				for (int j = 1; j <= m; j++) {
					f[i][j] = Math.max(f[i - 1][j], f[i][j - 1]) + w[i][j];
				}
			}

			System.out.println(f[n][m]);
		}
	}
}
```

