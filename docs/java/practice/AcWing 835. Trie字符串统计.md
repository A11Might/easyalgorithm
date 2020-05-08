[835. Trie字符串统计](https://www.acwing.com/problem/content/837/)

#### 算法：

*#Trie树*

#### 时间复杂度分析：



#### 代码：

```java
import java.util.*;

class Main {
    static final int N = 100010;
    static int idx;
    static int[][] son = new int[N][26];
    static int[] cnt = new int[N];
    
    static void insert(char[] str) {
        // 从根结点开始，0 号点既是根节点，又是空节点
        int p = 0;
        for (int i = 0; i < str.length; i++) {
            int u = str[i] - 'a';
            if (son[p][u] == 0) son[p][u] = ++idx;
            p = son[p][u];
        }
        cnt[p]++;
    }
    
    static int query(char[] str) {
        // 从根结点开始，0 号点既是根节点，又是空节点
        int p = 0;
        for (int i = 0; i < str.length; i++) {
            int u = str[i] - 'a';
            if (son[p][u] == 0) return 0;
            p = son[p][u];
        }
        return cnt[p];
    }
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        while (n-- > 0) {
            String op = sc.next();
            char[] str = sc.next().toCharArray();
            if (op.equals("I")) {
                insert(str);
            } else {
                System.out.println(query(str));
            }
        }
    }
}
```

