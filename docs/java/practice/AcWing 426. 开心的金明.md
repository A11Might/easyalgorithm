[426. 开心的金明](https://www.acwing.com/problem/content/428/)

#### 算法：

*DP* *背包问题*

**简化问题**

转化为 [01 背包问题](/java/practice/AcWing%202.%2001%E8%83%8C%E5%8C%85%E9%97%AE%E9%A2%98)

#### 时间复杂度分析：



#### 代码：

```java
import java.util.*;

class Main {
	static final int N = 30010;
	static int[] f = new int[N];

	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		int m = sc.nextInt(), n = sc.nextInt();

		for (int i = 0; i < n; i++) {
			int v = sc.nextInt(), p = sc.nextInt();
			for (int j = m; j >= v; j--) {
				f[j] = Math.max(f[j], f[j - v] + v * p);
			}
		}

		System.out.println(f[m]);
	}
}
```

