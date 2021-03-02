[734. 能量石](https://www.acwing.com/problem/content/736/)

#### 算法：

*贪心* *DP* *背包问题*

**贪心**

我们可以

- 选择吃哪些

  不吃变成零的，变成零的吃和不吃没有区别

- 按照什么顺序吃

这两维可以组合出所有吃的方式。

对于任意可能方案中的任意两个相邻能量石 i, i + 1：

- 先吃 i：E'<sub>i</sub> + E'<sub>i + 1</sub> - S<sub>i</sub> * L<sub>i + 1</sub>
- 先吃 i + 1：E'<sub>i + 1</sub> + E'<sub>i </sub> - S<sub>i + 1</sub> * L<sub>i</sub>

当 S<sub>i</sub> * L<sub>i + 1</sub> < S<sub>i + 1</sub> * L<sub>i</sub> ，也就是 S<sub>i</sub> / L<sub>i</sub> < S<sub>i + 1</sub> / L<sub>i + 1</sub>，先吃 i 可以获得更高的能量。

所以对所有物品按照这样的定义从小到大进行排序，这样从前往后吃一定是最优的。

**状态表示 - f(i, j)**

状态表示是针对按照比值从小到大的顺序吃来说的。

- 集合：所有只从前 i 块能量石中选，且总体积 `恰好` 是 j 的方案

  本题中能量的价值和时间是相关的，所以 j 需要表示精确值，而不能表示一个范围。所以不能改成 `不超过 j`。

- 属性：Max

**状态计算 - 集合划分**

f(i, j) = max(f(i - 1, j), f(i - 1, j - s[i]) + e[i] - (j - s[i]) * l[i])

在吃第 i 块能量石时，其所含能量为 `e[i] - (j - s[i]) * l[i])`：吃完第 i 个物品后的时间是 j，所以吃第 i 个物品前的时间是 j - s[i]，所以第 i 块能量石流逝的能量是 (j - s[i]) * l[i]。

#### 时间复杂度分析：



#### 代码：

```java
import java.util.*;

class Main {
	static final int N = 10010, INF = 0x3f3f3f3f;
	static int[][] stones = new int[N][3];
	static int[] f = new int[N];

	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		int T = sc.nextInt();
		for (int t = 1; t <= T; t++) {
			int n = sc.nextInt();
			int m = 0;
			for (int i = 0; i < n; i++) {
				stones[i][0] = sc.nextInt();
				stones[i][1] = sc.nextInt();
				stones[i][2] = sc.nextInt();
				m += stones[i][0];
			}

			Arrays.sort(stones, 0, n, (o1, o2) -> o1[0] * o2[2] - o2[0] * o1[2]);

			Arrays.fill(f, -INF);
			f[0] = 0;

			for (int i = 0; i < n; i++) {
				int s = stones[i][0], e = stones[i][1], l = stones[i][2];
				for (int j = m; j >= s; j--) {
					f[j] = Math.max(f[j], f[j - s] + e - (j - s) * l);
				}
			}
			
            // 因为状态的含义是“体积恰好为 j ”时的最大值，那就需要枚举体积。
			int ret = 0;
			for (int i = 0; i <= m; i++) ret = Math.max(ret, f[i]);
			System.out.printf("Case #%d: %d\n", t, ret);
		}
	}
}
```

