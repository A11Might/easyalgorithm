[482. 合唱队形](https://www.acwing.com/problem/content/484/)

#### 算法：

*DP* *LIS*

与 [1014. 登山](java/practice/AcWing%201014.%20登山) 相同。

#### 时间复杂度分析：



#### 代码：

```java
import java.util.*;

class Main {
	static final int N = 1010;
	static int n;
	static int[] h = new int[N];
	static int[] f = new int[N], g = new int[N];

	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		n = sc.nextInt();
		for (int i = 1; i <= n; i++) h[i] = sc.nextInt();

		for (int i = 1; i <= n; i++) {
			f[i] = 1;
			for (int j = 1; j < i; j++) {
				if (h[i] > h[j]) f[i] = Math.max(f[i], f[j] + 1);
			}
		}

		for (int i = n; i >= 1; i--) {
			g[i] = 1;
			for (int j = n; j > i; j--) {
				if (h[i] > h[j]) g[i] = Math.max(g[i], g[j] + 1);
			}
		}

		int ret = 0;
		for (int i = 1; i <= n; i++) {
			ret = Math.max(ret, f[i] + g[i] - 1);
		}
		System.out.println(n - ret);
	}
}
```

