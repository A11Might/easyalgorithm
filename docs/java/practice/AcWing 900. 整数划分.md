[900. 整数划分](https://www.acwing.com/problem/content/902/)

#### 算法：

*#DP#计数类DP*

##### 方法一

题目中规定了方案中元素的顺序（n<sub>1</sub> >= n<sub>2</sub> >= .. >= n<sub>k</sub>），也就是说 3 = 1 + 3 和 3 = 3 + 1 算是同一种方案，所以我们不用考虑顺序，只要选出一些数使得总和等于 n 就行了。

因此我们可以对问题进行抽象，将 n 看成一个大小为 n 的背包，不同正整数为物品，个数是无限个，这样问题就类似与完全背包了，不同的是 `本题需要正好填满大小为 n 背包 `。

**状态表示 - f(i, j)**

- 集合：所有从 1 ~ i 中选，且体积恰好是 j 的方案

- 属性：count

**状态计算 - 集合划分**

枚举第 i 个物品选几个来划分 f(i, j) 表示的集合：

- 不选第 i 个物品：f(i - 1, j)

- 选 1 个第 i 个物品：f(i - 1, j - i)

  ...

- 选 k 个第 i 个物品：f(i - 1, j - k * i)

综上：f(i, j) = f(i - 1, j) + f(i - 1, j - i) + ... f(i - 1, j - k * i)。

**优化**

类似完全背包的优化：

- f(i, j)       = f(i - 1, j) + f(i - 1, j - i) + ... f(i - 1, j - k * i)

- f(i, j - i) = 				   f(i - 1, j - i) + ... f(i - 1, j - k * i)，其中 k 是满足 k * i < j 的最大值，所以 j - (k + 1) * i 小于 0，也就是该状态不存在。

化简得到

f(i, j) = f(i - 1, j) + f(i, j - i)

##### 方法二

**状态表示 - f(i, j)**

- 集合：所有总和是 i，且恰好表示成 j 个数的和的方案

- 属性：count

**状态计算 - 集合划分**

- 方案中的最小值是 1

  总和是 i - 1，且恰好表示成 j - 1 个数的和的每个方案等价于总和是 i，恰好表示成 j 个数的和，并且方案中的最小值是 1 的每个方案都去掉一个 1，也就是说它们方案数是相同的：f(i - 1, j - 1)。

- 方案中的最小值大于 1

  因为方案中的最小值大于 1，所以方案中的每个数都减去 1 的话，每个数都还是正整数：f(i - j, j)，这两种状态的方案是一一对应的，所以方案数也是相同的。

综上，f(i, j) = f(i - 1, j - 1) + f(i - j, j)，所以答案 ans = f(n, 1) +  f(n, 2) + ... + f(n, n)。

#### 时间复杂度分析：



#### 代码：

##### 方法一

```java
import java.util.*;

class Main {
    static final int N = 1010, MOD = (int) 1e9 + 7;
    static int n;
    static int[] f = new int[N];
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        n = sc.nextInt();
        
        f[0] = 1;
        for (int i = 1; i <= n; i++) {
            for (int j = i; j <= n; j++) {
                f[j] = (f[j] + f[j - i]) % MOD;
            }
        }
        
        System.out.println(f[n]);
    }
}
```

##### 方法二

```java
import java.util.*;

class Main {
    static final int N = 1010, MOD = (int) 1e9 + 7;
    static int n;
    static int[][] f = new int[N][N];
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        n = sc.nextInt();
        
        f[0][0] = 1;
        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= i; j++) {
                f[i][j] = (f[i - 1][j - 1] + f[i - j][j]) % MOD;
            }
        }
        
        int ret = 0;
        for (int i = 1; i <= n; i++) ret = (ret + f[n][i]) % MOD;
        
        System.out.println(ret);
    }
}
```

