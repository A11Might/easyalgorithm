[837. 连通块中点的数量](https://www.acwing.com/problem/content/839/)

#### 算法：

*#并查集*

#### 时间复杂度分析：



#### 代码：

```java
import java.util.*;

class Main {
    static final int N = 100010;
    static int[] p = new int[N], cnt = new int[N];
    
    static int find(int x) {
        if (p[x] != x) p[x] = find(p[x]);
        return p[x];
    }
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt(), m = sc.nextInt();
        for (int i = 1; i <= n; i++) {
            p[i] = i;
            cnt[i] = 1;
        }
        
        while (m-- > 0) {
            String op = sc.next();
            int a, b;
            if (op.equals("C")) {
                a = sc.nextInt();
                b = sc.nextInt();
                a = find(a);
                b = find(b);
                // 当 a 和 b 在同一个连通块中则不能再连边，否则会使连通块中元素个数翻倍。
                if (a == b) continue;
                cnt[b] += cnt[a];
                p[a] = b;
            } else if (op.equals("Q1")) {
                a = sc.nextInt();
                b = sc.nextInt();
                if (find(a) == find(b)) System.out.println("Yes");
                else System.out.println("No");
            } else {
                a = sc.nextInt();
                System.out.println(cnt[find(a)]);
            }
        }
    }
}
```

