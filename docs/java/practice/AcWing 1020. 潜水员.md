[1020. 潜水员](https://www.acwing.com/problem/content/1022/)

#### 算法：

*DP* *背包问题*

**状态表示 - f(i, j, k)**

- 集合：所有从前 i 个物品中选，且氧气含量 `至少` 是 j，氮气含量 `至少` 是 k 的所有选法

- 属性：Min

**状态计算 - 集合划分**

以是否选取第 i 个物品来划分 f(i, j, k) 表示的集合：

- 所有不包含第 i 个物品的选法：f(i - 1, j, k)

- 所有包含第 i 个物品的选法：f(i - 1, j - v1[i], k - v2[i]) + w[i]

**Tips**

状态表示的三种情况

- 体积至多是 j：初始化时全部初始化为 0，计算时保证体积大于等于 0。

- 体积恰好是 j：初始化时 f(0, 0, 0) = 0, f(0, j, k) = +无穷，计算时保证体积大于等于 0。

  初始化为无穷的目的是在状态转移过程中不用这个不合法的状态。

- 体积至少是 j：初始化时 f(0, 0, 0) = 0, f(0, j, k) = +无穷，计算时不需要保证体积大于等于 0。

  因为体积是负数时状态是合法的，如 f(-2) 表示体积至少为 -2 的状态，体积可以是 5，也可以是 10，它等价于 f(0)。

#### 时间复杂度分析：



#### 代码：

```java
import java.util.*;

class Main {
	static final int M = 22, N = 80, INF = 0x3f3f3f3f;
	static int[][] f = new int[M][N];

	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		int m = sc.nextInt(), n = sc.nextInt(), K = sc.nextInt();

		for (int[] arr : f) Arrays.fill(arr, INF);
		f[0][0] = 0;

		for (int i = 0; i < K; i++) {
			int v1 = sc.nextInt(), v2 = sc.nextInt(), w = sc.nextInt();
			for (int j = m; j >= 0; j--) {
				for (int k = n; k >= 0; k--) {
                    // 因为气缸中气体的体积都是大于 0 的，所以负数状态和 0 状态是等价的
                    // 由于负数会越界，所以置成 0
					f[j][k] = Math.min(f[j][k], f[Math.max(0, j - v1)][Math.max(0, k - v2)] + w);
				}
			}
		}

		System.out.println(f[m][n]);
	}
}
```

