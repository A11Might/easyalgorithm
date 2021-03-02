[1027. 方格取数](https://www.acwing.com/problem/content/1029/)

#### 算法：

*DP* *数字三角形模型*

**化简问题**

如果只走一次的话：f(i, j) 表示所有从 (1, 1) 走到 (i, j) 的路径的最大值。

简单类比走两次的话：f(i<sub>1</sub>, j<sub>1</sub>, i<sub>2</sub>, j<sub>2</sub>) 表示所有从 (1, 1), (1, 1) 分别走到 (i<sub>1</sub>, j<sub>1</sub>), (i<sub>2</sub>, j<sub>2</sub>) 的路径的最大值。

那么如何处理 “同一个格子不能被重复选择”？

- 只有在 i<sub>1</sub> + j<sub>1</sub> == i<sub>2</sub> + j<sub>2</sub> 时，两条路径的格子才可能重合。

- 必要不充分
  - 格子重合时，一定有 i<sub>1</sub> + j<sub>1</sub> == i<sub>2</sub> + j<sub>2</sub>
  - i<sub>1</sub> + j<sub>1</sub> == i<sub>2</sub> + j<sub>2</sub> 时，格子不一定重合

综上，只有当两条路径的步数相同时，才有可能重合，所以我们可以使用一个 k 来表示每个步数相同的阶段，相当于让两个路径同时走。

**状态表示 - f(k, i<sub>1</sub>, i<sub>2</sub>)** 

- 集合：所有第一条路径从 (1, 1) 走到 (i<sub>1</sub>, k - i<sub>1</sub>)，第二条路径从 (1, 1) 走到 (i<sub>2</sub>, k - i<sub>2</sub>) 的路线组合的集合

- 属性：Max

其中，k 表示两条路径当前走到的格子的横纵坐标之和：k = i<sub>1</sub> + j<sub>1</sub> == i<sub>2</sub> + j<sub>2</sub>。

**状态计算 - 集合划分**

以最后一步来划分 f(k, i, j) 表示的集合：

- 第一条路径：向下；第二条路径：向下：f(k - 1, i<sub>1</sub> - 1, i<sub>2</sub> - 1) + t
  - 重合：t = w(i<sub>1</sub>, j<sub>1</sub>)
  
  - 不重合：t = w(i<sub>1</sub>, j<sub>1</sub>) + w(i<sub>2</sub>, j<sub>2</sub>)
  
- 第一条路径：向下；第二条路径：向右：f(k - 1, i<sub>1</sub> - 1, i<sub>2</sub>) + t

- 第一条路径：向右；第二条路径：向下：f(k - 1, i<sub>1</sub>, i<sub>2</sub> - 1) + t

- 第一条路径：向右；第二条路径：向右：f(k - 1, i<sub>1</sub>, i<sub>2</sub>) + t

综上：f(k, i<sub>1</sub>, i<sub>2</sub>) = max(f(k - 1, i<sub>1</sub> - 1, i<sub>2</sub> - 1), f(k - 1, i<sub>1</sub> - 1, i<sub>2</sub>), f(k - 1, i<sub>1</sub>, i<sub>2</sub> - 1), f(k - 1, i<sub>1</sub>, i<sub>2</sub>)) + t。

#### 时间复杂度分析：



#### 代码：

```java
import java.util.*;

class Main {
	static final int N = 15;
	static int n;
	static int[][] w = new int[N][N];
	static int[][][] f = new int[2 * N][N][N];

	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		n = sc.nextInt();
		int a = sc.nextInt(), b = sc.nextInt(), c = sc.nextInt();
		while (a != 0 || b != 0 || c != 0) {
			w[a][b] = c;
			a = sc.nextInt();
			b = sc.nextInt();
			c = sc.nextInt();
		}

		for (int k = 2; k <= 2 * n; k++) {
			for (int i1 = 1; i1 <= n; i1++) {
				for (int i2 = 1; i2 <= n; i2++) {
					int j1 = k - i1, j2 = k - i2;
					if (j1 >= 1 && j1 <= n && j2 >= 1 && j2 <= n) {
						int t = w[i1][j1];
						if (i1 != i2) t += w[i2][j2];
						f[k][i1][i2] = Math.max(
							Math.max(f[k - 1][i1 - 1][i2 - 1], f[k - 1][i1][i2]),
							Math.max(f[k - 1][i1 - 1][i2], f[k - 1][i1][i2 - 1])) + t;
					}					
				}
			}
		}

		System.out.println(f[2 * n][n][n]);
	}
}
```

