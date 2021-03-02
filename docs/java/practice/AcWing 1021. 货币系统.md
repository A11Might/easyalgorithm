[1021. 货币系统](https://www.acwing.com/problem/content/1023/)

#### 算法：

*DP* *背包问题*

**简化问题**

- n 种不同面值的货币看成 n 种不同的物品

- 面值为 m 的货币看成容量为 m 的背包

- 每个物品有无限个

可以转化为完全背包问题求方案数，与 [买书](java/practice/AcWing%201023.%20买书.md) 相同。

#### 时间复杂度分析：



#### 代码：

```java
import java.util.*;

class Main {
	static final int M = 3010;
	static long[] f = new long[M];

	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		int n = sc.nextInt(), m = sc.nextInt();

		f[0] = 1;
		for (int i = 0; i < n; i++) {
			int v = sc.nextInt();
			for (int j = v; j <= m; j++) {
				f[j] += f[j - v];
			}
		}

		System.out.println(f[m]);
	}
}
```

