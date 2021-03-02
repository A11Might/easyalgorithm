[8. 二维费用的背包问题](https://www.acwing.com/problem/content/8/)

#### 算法：

*DP* *背包问题*

**状态表示 - f(i, j, k)**

- 集合：所有只从前 i 个物品中选，并且总体积不超过 j，总重量不超过 k 的选法

- 属性：Max

**状态计算 - 集合划分**

以是否选取第 i 个物品来划分 f(i, j, k) 表示的集合：

- 所有不包含第 i 个物品的选法：f(i - 1, j, k)

- 所有包含第 i 个物品的选法：f(i - 1, j - v[i], k - m[i]) + w[i]

综上，f(i, j, k) = max(f(i - 1, j, k), f(i - 1, j - v[i], k - m[i]) + w[i])。

**注意**

二维费用可以分别和 01 背包、完全背包、多重背包、分组背包绑定。

类似的求方案数、求最小值也可以和所有背包问题绑定。

#### 时间复杂度分析：



#### 代码：

```java
import java.util.*;

class Main {
	static final int N = 110;
	static int[][] f = new int[N][N];

	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		int n = sc.nextInt(), V = sc.nextInt(), M = sc.nextInt();

		for (int i = 0; i < n; i++) {
			int v = sc.nextInt(), m = sc.nextInt(), w = sc.nextInt();
			for (int j = V; j >= v; j--) {
				for (int k = M; k >= m; k--) {
					f[j][k] = Math.max(f[j][k], f[j - v][k - m] + w);
				}
			}
		}

		System.out.println(f[V][M]);
	}
}
```

