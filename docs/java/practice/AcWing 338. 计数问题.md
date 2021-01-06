[338. 计数问题](https://www.acwing.com/problem/content/340/)

#### 算法

*#DP#数位统计类DP*

**简化问题**

计算 [a, b] 中数字 0 ~ 9 出现的次数，我们可以先定义 count(n, x) 计算 [1, n] 中数字 x 出现的次数，这样类似于前缀和，[a, b] 中数字 x 出现的次数就等于 count(b, x) - count(a - 1, x)，题目就转化为计算从 [1, n] 中数字 x 出现的次数。

**分情况讨论**

计算 [1, n] 中 1 出现的次数时，我们可以分别求出 1 在每一位上出现的次数，然后累加来求，其中 n 使用 abcdefg 表示。

以求 1 在第 4 为上出现的次数为例，1 <= xxx1yyy <= abcdefg：

- 当 xxx 取 [000, abc - 1] 时，yyy 可以取到 [000, 999]，所以 1 出现次数为 abc * 1000。

- 当 xxx 取 abc 时 

  - 如果 d < 1 的话，abc1yyy > abc0efg，所以 1 出现次数为 0。
  
  - 如果 d = 1 的话，yyy 可以取到 [000, efg]，所以 1 出现次数为 efg + 1。
  
  - 如果 d > 1 的话，yyy 可以取到 [000, 999]，所以 1 出现次数为 1000。

**边界情况：**

- 当数字 x 出现在第一位时，就没有第一种情况。
- 当数字 x 是 0 时，在第一种情况中可能取 000，导致出现前导 0，所以 xxx 只能取 1 ~ abc - 1。

#### 时间复杂度分析：



#### 代码：

```java
import java.util.*;

class Main {
    static final int N = 10;
    static int a, b;
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        a = sc.nextInt();
        b = sc.nextInt();
        while (a != 0 || b != 0) {
            if (a > b) {
                int tmp = b;
                b = a;
                a = tmp;
            }
            
            for (int i = 0; i <= 9; i++) {
                System.out.print((count(b, i) - count(a - 1, i)) + " ");
            }
            System.out.println();
            
            a = sc.nextInt();
            b = sc.nextInt();
        }
        
    }
    
    static int count(int n, int x) {
        if (n == 0) return 0;
        
        // 将 n 按位拆分成数字，低位到高位
        List<Integer> num = new ArrayList<>();
        while (n != 0) {
            num.add(n % 10);
            n /= 10;
        }
        n = num.size();
        
        int ret = 0;
        for (int i = n - 1; i >= 0; i--) {
            // 0 在最高位时其为先导 0，需要跳过
            if (x == 0 && i == n - 1) continue;
            // case 1
            if (i < n - 1) {
                ret += get(num, i + 1, n - 1) * power10(i);
                if (x == 0) ret -= power10(i);
            }
            // case 2
            if (num.get(i) == x) ret += get(num, 0, i - 1) + 1;
            else if (num.get(i) > x) ret += power10(i); 
        }
        
        return ret;
    }
    
    static int get(List<Integer> num, int l, int r) {
        int ans = 0;
        for (int i = r; i >= l; i--) ans = ans * 10 + num.get(i);
        return ans;
    }
    
    static int power10(int i) {
        int ans = 1;
        while (i-- > 0) ans *= 10;
        return ans;
    }
}
```

