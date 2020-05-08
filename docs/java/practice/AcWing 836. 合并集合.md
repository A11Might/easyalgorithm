[836. 合并集合](https://www.acwing.com/problem/content/838/)

#### 算法：

*#并查集*

#### 时间复杂度分析：



#### 代码：

```java
import java.util.*;

class Main {
    static final int N = 100010;
    static int[] p = new int[N];
    
    static int find(int x) {
        if (p[x] != x) p[x] = find(p[x]);
        return p[x];
    }
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt(), m = sc.nextInt();
        for (int i = 0; i <= n; i++) p[i] = i;
        
        while (m-- > 0) {
            String op = sc.next();
            int a = sc.nextInt(), b = sc.nextInt();
            if (op.equals("M")) {
                p[find(a)] = find(b);
            } else {
                if (find(a) == find(b)) System.out.println("Yes");
                else System.out.println("No");
            }
        }
    }
}
```

