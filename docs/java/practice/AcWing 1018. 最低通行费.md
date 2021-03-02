[1018. 最低通行费](https://www.acwing.com/problem/content/1020/)

#### 算法：

*DP* *数字三角形模型*

**化简问题**

商人必须在 (2n - 1) 个单位时间穿越出去，表示商人不能走回头路：1 + 2 * (n - 1)，所以本题就转化为 [1015. 摘花生](java/practice/AcWing%201015.%20摘花生.md)。

与摘花生不同的是：本题求的是最小值，所以第一列不能从左边转移过来，第一行不能从上面转移过来，因为它们都是 0，求 min 的时候可能会被取到。

#### 时间复杂度分析：



#### 代码：

```java
import java.util.*;

class Main {
	static final int N = 110, INF = 0x3f3f3f3f;
	static int n;
	static int[][] w = new int[N][N];
	static int[][] f = new int[N][N];

	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		n = sc.nextInt();
		for (int i = 1; i <= n; i++) {
			for (int j = 1; j <= n; j++) {
				w[i][j] = sc.nextInt();
			}
		}

		for (var col : f) Arrays.fill(col, INF);

		for (int i = 1; i <= n; i++) {
			for (int j = 1; j <= n; j++) {
				if (i == 1 && j == 1) f[i][j] = w[i][j]; // 特判左上角
				if (i > 1) f[i][j] = Math.min(f[i][j], f[i - 1][j] + w[i][j]); // 只有不在第一行的时候，才可以从上面过来
				if (j > 1) f[i][j] = Math.min(f[i][j], f[i][j - 1] + w[i][j]); // 只有不在第一列的时候，才可以从左边过来
			}
		}

		System.out.println(f[n][n]);
	}
}
```

