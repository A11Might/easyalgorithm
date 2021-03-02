[275. 传纸条](https://www.acwing.com/problem/content/277/)

#### 算法：

*DP* *数字三角形模型*

**化简问题**

与 [1027. 方格取数](java/practice/AcWing%201027.%20方格取数) 相同。

#### 时间复杂度分析：



#### 代码：

```java
import java.util.*;

class Main {
	static final int N = 55;
	static int n, m;
	static int[][] g = new int[N][N];
	static int[][][] f = new int[2 * N][N][N];

	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		n = sc.nextInt();
		m = sc.nextInt();
		for (int i = 1; i <= n; i++) {
			for (int j = 1; j <= m; j++) {
				g[i][j] = sc.nextInt();
			}
		}

		for (int k = 2; k <= n + m; k++) {
			for (int i1 = 1; i1 <= n; i1++) {
				for (int i2 = 1; i2 <= n; i2++) {
					int j1 = k - i1, j2 = k - i2;
					if (j1 >= 1 && j1 <= m && j2 >= 1 && j2 <= m) {
						int t = g[i1][j1];
						if (i1 != i2) t += g[i2][j2];
						f[k][i1][i2] = Math.max(
							Math.max(f[k - 1][i1 - 1][i2 - 1], f[k - 1][i1][i2]),
							Math.max(f[k - 1][i1 - 1][i2], f[k - 1][i1][i2 - 1])) + t;
					}
				}
			}
		}

		System.out.println(f[n + m][n][n]);
	}
}
```

