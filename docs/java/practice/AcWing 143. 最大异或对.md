[143. 最大异或对](https://www.acwing.com/problem/content/145/)

#### 算法：

*#Trie树*

**朴素算法（O(n<sup>2</sup>)）**

因为 ax ^ ay 和 ay ^ ax 是一样的，所有我们可以固定顺序来枚举：第二个枚举的数的索引小于第一个。

```java
int ret = 0;

for (int i = 0; i < n; i++) { // 枚举第一个数
    for (int j = 0; j < i; j++) { // 枚举第二个数
        ret = Math.max(ret, a[i] ^ a[j]);
    }
}
```

**优化**

题目数据范围为 0 ≤ A<sub>i</sub> < 2<sup>31</sup>，也就是说每个整数都可以转化成为一个 32 位的二进制数，这样我们就可以将整数的二进制数当做字符串，按高位到低位的顺序存入前缀树中。

当我们枚举寻找与当前元素 ai 异或最大的元素时，可以直接在前缀树中搜索：每次都走与 ai 这一位相反的位置走（这样异或和最大），如果没有路可以走的话，就走相同的路，直到走到叶子结点时，就找到了与当前元素 ai 异或最大的元素。

#### 时间复杂度分析：



#### 代码：

```java
import java.util.*;

class Main {
    static final int N = 100010, M = 31 * N;
    static int idx;
    static int[][] son = new int[M][2];

    static void insert(int x) {
        int p = 0;
        for (int i = 30; i >= 0; i--) {
            int u = x >> i & 1;
            if (son[p][u] == 0) son[p][u] = ++idx;
            p = son[p][u];
        }
    }

    static int search(int x) {
        int p = 0, ret = 0;
        for (int i = 30; i >= 0; i--) {
            int u = x >> i & 1;
            if (son[p][1 - u] != 0) {
                // 如果当前子树中，存在第 i 位和 x 的第 i 位不同的数，说明答案的第 i 位可以变成 1，就把 res 的第 i 位二进制位变成1
                ret += 1 << i;
                p = son[p][1 - u];
            } else p = son[p][u];
        }
        return ret;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();

        int ret = 0;
        while (n-- > 0) {
            int x = sc.nextInt();
            // 将插入和查找放在一起，可以不用使用额外数组存储给定序列
            // 虽然 x ^ x = 0，可以先查找再插入
            // 但是先插入再查找，可以不用在树空的时候特判
            insert(x);
            ret = Math.max(ret, search(x));
        }

        System.out.println(ret);
    }
}
```

