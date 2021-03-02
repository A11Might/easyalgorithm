[1013. 机器分配](https://www.acwing.com/problem/content/1015/)

#### 算法：

*DP* *背包问题*

**简化问题**

- 将每个公司看成一组物品，公司数量 n 就是物品的组数

- 将每个公司分几台机器看成每组中的不同物品，总机器数 m 就是每组物品中的物品种数（因为矩阵中的第 i 行第 j 列的整数表示第 i 个公司分配 j 台机器时的盈利，矩阵一共有 m 列）

- 每个公司分配机器的个数就是每个物品的体积，总机器数 m 也是最大容积，价值就是价值


这样我们就将问题转化为[分组背包问题](/java/practice/AcWing%209.%20%E5%88%86%E7%BB%84%E8%83%8C%E5%8C%85%E9%97%AE%E9%A2%98)。

#### 时间复杂度分析：



#### 代码：

```java
import java.util.*;

class Main {
	static final int N = 11, M = 16;
	static int[][] w = new int[N][M];
	static int[][] f = new int[N][M];
	static int[] way = new int[N];

	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		int n = sc.nextInt(), m = sc.nextInt();

		for (int i = 1; i <= n; i++) {
			for (int j = 1; j <= m; j++) {
				w[i][j] = sc.nextInt();
			}
		}

		for (int i = 1; i <= n; i++) { // 物品，枚举每组物品
			for (int j = 0; j <= m; j++) { // 体积，枚举体积
				for (int k = 0; k <= j; k++) { // 决策，枚举每个物品
					f[i][j] = Math.max(f[i][j], f[i - 1][j - k] + w[i][k]);
				}
			}
		}

		System.out.println(f[n][m]);

		for (int i = n, j = m; i > 0; i--) {
			for (int k = 0; k <= j; k++) { // 看状态 f(i, j) 是从哪个状态转移过来的
				if (f[i][j] == f[i - 1][j - k] + w[i][k]) {
					way[i] = k;
					j -= k;
					break;
				}
			}
		}

		for (int i = 1; i <= n; i++) System.out.println(i + " " + way[i]);
	}
}
```

