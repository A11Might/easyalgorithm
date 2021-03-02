[1017. 怪盗基德的滑翔翼](https://www.acwing.com/problem/content/1019/)

#### 算法：

*DP* *LIS*

**简化问题**

当起点和方向确定后，最长的距离就是以起点为结尾的 [895. 最长上升子序列](java/practice/AcWing%20895.%20最长上升子序列)。

#### 时间复杂度分析：



#### 代码：

```java
import java.util.*;

class Main {
	static final int N = 110;
	static int n;
	static int[] h = new int[N];
	static int[] f = new int[N];

	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		int T = sc.nextInt();
		while (T-- > 0) {
			n = sc.nextInt();
			for (int i = 1; i <= n; i++) h[i] = sc.nextInt();

            int ret = 0;
			for (int i = 1; i <= n; i++) {
				f[i] = 1;
				for (int j = 1; j < i; j++) {
					if (h[i] > h[j]) f[i] = Math.max(f[i], f[j] + 1);
				}
				ret = Math.max(ret, f[i]);
			}

			Arrays.fill(f, 0);
			for (int i = n; i >= 1; i--) {
				f[i] = 1;
				for (int j = n; j > i; j--) {
					if (h[i] > h[j]) f[i] = Math.max(f[i], f[j] + 1);
				}
				ret = Math.max(ret, f[i]);
			}

			System.out.println(ret);
		}
	}
}
```

