[841. 字符串哈希](https://www.acwing.com/problem/content/843/)

#### 算法：

*#字符串哈希*

#### 时间复杂度分析：



#### 代码：

```java
import java.util.*;

class Main {
    static final int N = 100010, P = 131;
    static final long mod = Long.MAX_VALUE;
    static long[] h = new long[N], p = new long[N];

    static long get(int l, int r) {
        return h[r] - h[l - 1] * p[r - l + 1];
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt(), m = sc.nextInt();
        char[] str = (" " + sc.next()).toCharArray();

        // 预处理
        p[0] = 1;
        for (int i = 1; i <= n; i++) {
            p[i] = p[i - 1] * P;
            h[i] = (h[i - 1] * P + str[i]) % mod;
        }

        while (m-- > 0) {
            int a =sc.nextInt(), b = sc.nextInt(), c = sc.nextInt(), d = sc.nextInt();
            if (get(a, b) == get(c, d)) System.out.println("Yes");
            else System.out.println("No");
        }
    }
}
```

