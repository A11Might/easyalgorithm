[828. 模拟栈](https://www.acwing.com/problem/content/830/)

#### 算法：

*#栈*

#### 时间复杂度分析：



#### 代码：

```java
import java.util.*;

class Main {
    static final int N = 100010;
    static int tt;
    static int[] stk = new int[N];
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int m = sc.nextInt();
        while (m-- > 0) {
            int x;
            String op = sc.next();
            if (op.equals("push")) {
                x = sc.nextInt();
                stk[++tt] = x;
            } else if (op.equals("pop")) {
                tt--;
            } else if (op.equals("query")) {
                System.out.println(stk[tt]);
            } else {
                if (tt == 0) System.out.println("YES");
                else System.out.println("NO");
            }
        }
    }
}
```

