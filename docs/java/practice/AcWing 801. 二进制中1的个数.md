[801. 二进制中1的个数](https://www.acwing.com/problem/content/803/)

#### 算法：

*#位运算*

每次减去给定整数 x 二进制中的最后一位 1（lowbit(n) = n & -n），一共能减几次 x 二进制中就有几个 1。

#### 时间复杂度分析：



#### 代码：

```java
import java.util.*;

class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        while (n-- > 0) {
            int x = sc.nextInt(), cnt = 0;
            while (x != 0) {
                x -= x & -x;
                cnt++;
            }
            System.out.print(cnt + " ");
        }
    }
}
```

