[5. 多重背包问题 II](https://www.acwing.com/problem/content/5/)

#### 算法：

*#DP#背包问题*

朴素做法的三重循环时间复杂度 O(n * v * s)，等于 40 亿，一定会超时，所以需要优化。

但无法像完全背包一样优化，因为：

f(i, j) = max(f(i - 1, j), f(i - 1, j - v[i]) + w[i], f(i - 1, j - 2 * v[i]) + 2 * w[i], ..., f(i - 1, j - s[i] * v[i]) + s[i] * w[i])

f(i, j - v[i]) = max(      f(i - 1, j - v[i]),            f(i - 1, j - 2 * v[i]) + w[i], ...,       f(i - 1, j - s[i] * v[i]) + (s[i] - 1) * w[i], f(i - 1, j - (s[i] + 1) * v[i]) + s[i] * w[i])

f(i, j - v[i]) 会比 f(i, j) 的后面多出一项，所以无法使用 f(i, j - v[i]) 的最大值来得到 f(i, j) 后半部分的最大值，也就是无法像完全背包一样优化。

**二进制优化：**

假设第 i 个物品有 k 个，我们不需要从 0 开始一直枚举到 k，可以使用一种更高效的方式：将若干个第 i 个物品打包在一起，一块考虑。

比如，将第 i 个物品打包成 1, 2, 4, 8, ...，若干个不同的组，每组只能选一次，我们可以使用这些不同的组拼出 k 中的任何一个数。这样每一组打包起来的第 i 个物品，可以看成 0 1 背包中的一个物品，相当于使用若干个新的物品来表示原来的第 i 个物品。

#### 时间复杂度分析：

我们先将每种物品拆分成不同组，然后使用 01 背包。每种物品的个数为 s，拆分成不同组就是 logs，一共 n 种物品，所以一共有 n * logs 个物品，总时间复杂度为 n * logs * v，不会超时。

#### 代码：

```java
import java.util.*;

class Main {
    static final int N = 12010, M = 2010;
    static int n, m;
    static int[] v = new int[N], w = new int[N];
    static int[] f = new int[N];
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        n = sc.nextInt();
        m = sc.nextInt();
        // 打包物品
        int idx = 0; // 打包后物品的编号
        for (int i = 1; i <= n; i++) {
            int a = sc.nextInt(), b = sc.nextInt(), s = sc.nextInt();
            // k 表示打包后的第 idx 个物品的包含原始物品的个数
            int k = 1;
            while (s - k >= 0) {
                idx++;
                v[idx] = k * a;
                w[idx] = k * b;
                s -= k;
                k *= 2;
            }   
            // 剩余原始物品再打包成一个
            if (s > 0) {
                idx++;
                v[idx] = s * a;
                w[idx] = s * b;
            }
        }
        n = idx;
        
        for (int i = 1; i <= n; i++) {
            for (int j = m; j >= v[i]; j--) {
                f[j] = Math.max(f[j], f[j - v[i]] + w[i]);
            }
        }
        
        System.out.println(f[m]);
    }
}
```

