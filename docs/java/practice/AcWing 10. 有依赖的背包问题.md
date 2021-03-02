[10. 有依赖的背包问题](https://www.acwing.com/problem/content/10/)

#### 算法：

*DP* *背包问题*

**状态表示 - f(u, j)**

- 集合：所有从以 u 为根的子树中选，且总体积不超过 j 的方案

- 属性：Max

**状态计算 - 集合划分**

以节点 u 的子树来划分 f(u, j) 表示的集合：

- 子树 1

  以体积来划分子树 1 表示的集合：

  - 体积为 0 时的最大价值

  - 体积是 1 时的最大价值

    ...

  - 体积是 m 时的最大价值

  与 [金明的预算方案](java/practice/AcWing%20487.%20金明的预算方案.md) 以方案的划分不同，假设有 3 个附件的话就是有 2<sup>3</sup> 种方案。但这里的话，子树的节点个数很多，最多有 100 个节点，如果我们以方案来划分的话，最多有 2<sup>100</sup> 种选法，这是没法存的，所有这里以体积来划分。

- 子树 2

- 子树 3

  ...

每个子树相当于一组物品，每组中有 m + 1 个物品（第 0 个物品表示体积是 0、价值是 f(0)，...），只能从每组物品中选取一个物品，问可以获取的最大价值，所以在递归考虑每一个子树时，就转化为一个分组背包问题。

#### 时间复杂度分析：

所有的子节点总和是n，所以总时间复杂度是 O(n<sup>3</sup>)。

#### 代码：

```java
import java.util.*;

class Main {
	static final int N = 110;
	static int n, m;
	static int[] v = new int[N], w = new int[N];
	static int h[] = new int[N], e[] = new int[N], ne[] = new int[N], idx;
	static int[][] f = new int[N][N];

	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		n = sc.nextInt();
		m = sc.nextInt();

		Arrays.fill(h, -1);
		int root = 0;
		for (int i = 1; i <= n; i++) {
			v[i] = sc.nextInt();
			w[i] = sc.nextInt();
			int p = sc.nextInt();
			if (p == -1) root = i;
			else add(p, i);
		}

		dfs(root);

		System.out.println(f[root][m]);
	}

	static void add(int a, int b) {
		e[idx] = b;
		ne[idx] = h[a];
		h[a] = idx++;
	}

	static void dfs(int u) {
		for (int i = h[u]; i != -1; i = ne[i]) { // 循环物品组
			int son = e[i];
			dfs(son);

			// 分组背包
			for (int j = m - v[u]; j >= 0; j--) { // 循环体积
				for (int k = 0; k <= j; k++) { // 循环决策
					f[u][j] = Math.max(f[u][j], f[u][j - k] + f[son][k]);
				}
			}
		}

		// 将物品 u 加进去
		for (int i = m; i >= v[u]; i--) f[u][i] = f[u][i - v[u]] + w[u];
		for (int i = 0; i < v[u]; i++) f[u][i] = 0;
	}
}
```

