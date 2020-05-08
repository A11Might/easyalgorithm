[829. 模拟队列](https://www.acwing.com/problem/content/831/)

#### 算法：

*#队列*

#### 时间复杂度分析：



#### 代码：

```java
import java.util.*;

class Main {
    static final int N = 100010;
    static int hh, tt;
    static int[] q = new int[N];
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        hh = 0;
        tt = -1;
        
        int m = sc.nextInt();
        while (m-- > 0) {
            int x;
            String op = sc.next();
            if (op.equals("push")) {
                x = sc.nextInt();
                q[++tt] = x;
            } else if (op.equals("pop")) {
                hh++;
            } else if (op.equals("query")) {
                System.out.println(q[hh]);
            } else {
                if (tt < hh) System.out.println("YES");
                else System.out.println("NO");
            }
        }
    }
}
```

