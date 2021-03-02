[1016. 最大上升子序列和](https://www.acwing.com/problem/content/1018/)

#### 算法：

*DP* *LIS*

**状态表示 - f(i)**

- 集合：所有以 a[i] 结尾的上升子序列

- 属性：Max（与 [895. 最长上升子序列](java/practice/AcWing%20895.%20最长上升子序列) 不同，这里是 `和的最大值`）

**状态计算 - 集合划分**

以倒数第二个数来划分 f(i) 表示集合：

- 倒数第二个数不存在：a[i]

- 倒数第二个数是 a[1]

- 倒数第二个数是 a[2]

  ...

- 倒数第二个数是 a[k]：f(k) + a[k]

综上，f(i) = max(f(k) + a[k]) if a[k] < a[i]。

#### 时间复杂度分析：



#### 代码：

```java
import java.util.*;

class Main {
	static final int N = 1010;
	static int n;
	static int[] w = new int[N];
	static int[] f = new int[N];

	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		n = sc.nextInt();
		for (int i = 1; i <= n; i++) w[i] = sc.nextInt();

		int ret = 0;
		for (int i = 1; i <= n; i++) {
			f[i] = w[i];
			for (int j = 1; j < i; j++) {
				if (w[i] > w[j]) {
					f[i] = Math.max(f[i], f[j] + w[i]);
				}
			}
			ret = Math.max(ret, f[i]);
		}

		System.out.println(ret);
	}
}
```

