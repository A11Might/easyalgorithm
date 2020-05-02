[902. 最短编辑距离](https://www.acwing.com/problem/content/904/)

#### 算法：

*#DP#线性DP*

**状态表示 - f(i, j)**

- 集合：所有将 a[1 ~ i] 变成 b[1 ~ j] 的操作方式。
- 属性：Min

**状态计算 - 集合划分**

- 按照最后一步的操作来划分 f(i, j) 表示的集合：
  - 最后一步的操作是删除 a[i]

    删除 a[i] 后使两字符串相同的最少操作步数就是将 a[1 ~ i - 1] 变成 b[1 ~ j] 的最少操次数，然后再加上删除的这步，f(i - 1, j) + 1。

  - 最后一步的操作是增加

    在 a 的末尾添加一个字符使两字符串相同的最少操作步数就是将 a[1 ~ i] 变成 b[1 ~ j - 1]，然后将再在 a 中添加一个与 b[j] 相同的字符，f(i, j - 1) + 1。

  - 最后一步的操作是修改 a[i]

    - a[i] 与 b[j] 相同时：只要将 a[1 ~ i - 1] 变成 b[1 ~ j - 1] 就行了，a[i] 和 b[j] 是相同的不用操作，f(i - , j - 1)。

    - a[i] 与 b[j] 不相同时：则需要将 a[1 ~ i - 1] 变成 b[1 ~ j - 1] 后，再将 a[i] 修改成 b[j]，f(i - , j - 1) + 1。

  综上，f(i, j) = min(f(i - 1, j) + 1, f(i, j - 1) + 1, f(i - 1, j - 1) + 1, f(i - 1, j - 1) if a[i] == b[j])。
  
- 按到 a[i] 和 b[j] 是否相同来划分 f(i, j) 表示的集合：

  - a[i] 和 b[j] 相同

    只需将 a[1 ~ i - 1] 变成 b[1 ~ j - 1] 就行了，a[i] 和 b[j] 相同的不需要进行操作，f(i - 1, j - 1)。

  - a[i] 和 b[j] 不同

    - 删除 a[i]，f(i - 1, j) + 1。
    - 在 a 中添加一个与 b[j] 相同的字符，f(i, j - 1) + 1。
    - 将 a[i] 修改成 b[j]，f(i - 1, j - 1) + 1。

  综上，f(i, j) = min(f(i - 1, j) + 1, f(i, j - 1) + 1, f(i - 1, j - 1) + 1, f(i - 1, j - 1) if a[i] == b[j])。

#### 时间复杂度分析：

状态数是 n<sup>2</sup>，计算每个状态需要 3 次运算，所以时间复杂度是 O(n<sup>2</sup>)。

#### 代码：

```java
import java.util.*;

class Main {
    static final int N = 1010;
    static int n, m;
    static char[] a = new char[N], b = new char[N];
    static int[][] f = new int[N][N];
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        n = sc.nextInt();
        a = (" " + sc.next()).toCharArray();
        m = sc.nextInt();
        b = (" " + sc.next()).toCharArray();
        
        for (int i = 0; i <= n; i++) f[i][0] = i;
        for (int j = 0; j <= m; j++) f[0][j] = j;
        
        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= m; j++) {
                if (a[i] == b[j]) f[i][j] = f[i -1][j - 1];
                else f[i][j] = Math.min(f[i - 1][j - 1], Math.min(f[i - 1][j], f[i][j - 1])) + 1;
            }
        }
        
        System.out.println(f[n][m]);
    }
}
```

