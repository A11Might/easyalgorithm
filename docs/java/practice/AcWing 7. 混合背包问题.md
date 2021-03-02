[7. 混合背包问题](https://www.acwing.com/problem/content/7/)

#### 算法：

*DP* *背包问题*

**状态表示 - f(i, j)**

- 集合：只从前 i 个物品中选，且总体积不超过 j 的选法

- 属性：Max

**状态计算 - 集合划分**

- 01 背包：f(i, j) = max(f(i - 1, j), f(i - 1, j - v[i]) + w[i])

- 完全背包：f(i, j) = max(f(i -1, j), f(i, j - v[i]) + w[i])

- 多重背包：f(i, j) = max(f(i - 1, j), f(i - 1, j - v[i]) + w[i], f(i - 1, j - 2 * v[i]) + 2 * w[i], ...)

状态表示时我们没有考虑前 i 个物品的类型，所以在状态计算时我们只需要用到第 i 个物品的类型，通过物品类型判断使用哪种状态转移方程。

**Tips**

01 背包是特殊的多重背包：物品个数都为 1 的多重背包问题。

#### 时间复杂度分析：



#### 代码：

```java
import java.util.*;

class Main {
	static final int N = 1010;
	static int[] f = new int[N];

	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		int n = sc.nextInt(), m = sc.nextInt();

		for (int i = 0; i < n; i++) {
			int v = sc.nextInt(), w = sc.nextInt(), s = sc.nextInt();
			if (s == 0) {
				for (int j = v; j <= m; j++) {
					f[j] = Math.max(f[j], f[j - v] + w);
				}
			} else {
				if (s == -1) s = 1;
				for (int j = m; j >= v; j--) {
					for (int k = 0; k <= s && k * v <= j; k++) {
						f[j] = Math.max(f[j], f[j - k * v] + k * w);
					}
				}
			}
		}

		System.out.println(f[m]);
	}
}
```

