[11. 背包问题求方案数](https://www.acwing.com/problem/content/11/)

#### 算法：

*DP* *背包问题*

题目问的是最有选法的方案数，并不是装满背包的方案数，而是最大价值的方案数

**状态表示 - f(i, j)**

从前 i 个物品中选，且体积 `恰好` 是 j 的所有选法中可以获得最大价值（恰好比较好算，使用至少的话需要用到容斥原理）

**状态转移 - 集合划分**

f(i, j) = max(f(i - 1, j), f(i - 1, j - v[i]) + w[i])

使用数组 g(i, j) 存储 f(i, j) 取最大值的方案数

- 左边大：g(i - 1, j)

  右边所有方案的最大值都是小于左边的，所以右边的方案数就是 0

- 右边大：g(i - 1, j - v[i])

- 一样大：g(i - 1, j) + g(i - 1, j - v[i])

**Tips**

在一般的背包问题中，状态表示的方式不仅可以定义成 `不超过` j，也都是可以定义成 `恰好` 为 j 的。

`恰好` 和 `最多` 只有在初始化和算答案的时候不同，时刻抓住状态表示的含义即可。恰好在初始化的时候f[0, 0] = 0，其余f[0, i] = -INF。

#### 时间复杂度分析：



#### 代码：

```java
import java.util.*;

class Main {
	static final int N = 1010, MOD = (int)1e9 + 7, INF = 0x3f3f3f3f;
	static int[] f = new int[N], g = new int[N];

	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		int n = sc.nextInt(), m = sc.nextInt();

		Arrays.fill(f, -INF);
		f[0] = 0;
		g[0] = 1;

		for (int i = 0; i < n; i++) {
			int v = sc.nextInt(), w = sc.nextInt();
			for (int j = m; j >= v; j--) {
				int maxv = Math.max(f[j], f[j - v] + w);
				int cnt = 0;
				if (maxv == f[j]) cnt += g[j];
				if (maxv == f[j - v] + w) cnt += g[j - v];
				f[j] = maxv;
				g[j] = cnt % MOD;				
			}
		}

		int maxv = 0; // 最大价值
		for (int i = 1; i <= m; i++) maxv = Math.max(maxv, f[i]);

		int cnt = 0; // 最大价值的方案数
		for (int i = 1; i <= m; i++) {
			if (f[i] == maxv) cnt = (cnt + g[i]) % MOD;
		}
		System.out.println(cnt);
	}
}
```

