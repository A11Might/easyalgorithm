[847. 图中点的层次](https://www.acwing.com/problem/content/849/)

#### 算法：

*#bfs*

所有边的长度都是 1 ，使用 bfs 求最短路径。

#### 时间复杂度分析：



#### 代码：

```java
import java.util.*;

class Main {
    static final int N = 100010;
    static int n, m;
    static int[] h = new int[N], e = new int[N], ne = new int[N], idx;
    static int[] q = new int[N], d = new int[N]; // 数组 d 记录每个节点距离 1 号点的距离
    
    
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        n = sc.nextInt();
        m = sc.nextInt();
        
        Arrays.fill(h, -1);
        for (int i = 0; i < m; i++) {
            int a = sc.nextInt(), b = sc.nextInt();
            add(a, b);
        }
        
        bfs();
        System.out.println(d[n]);
    }
    
    static void add(int a, int b) {
        e[idx] = b;
        ne[idx] = h[a];
        h[a] = idx++;
    }
    
    static void bfs() {
        int hh = 0, tt = -1;
        // 将每个点的距离初始化为 -1，标记为未访问
        Arrays.fill(d, -1);
        q[++tt] = 1;
        d[1] = 0;
        while (tt >= hh) {
            int u = q[hh++];
            for (int i = h[u]; i != -1; i = ne[i]) {
                int j = e[i];
                if (d[j] != -1) continue;
                d[j] = d[u] + 1;
                q[++tt] = j;
            }
        }
    }
}
```

