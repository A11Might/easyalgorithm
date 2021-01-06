[870. 约数个数](https://www.acwing.com/problem/content/872/)

#### 算法：



#### 时间复杂度分析：



#### 代码：

```java
import java.util.*;

class Main {
    static final int MOD = (int) 1e9 + 7;
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        
        HashMap<Integer, Integer> primes = new HashMap<>();
        while (n-- > 0) {
            int a = sc.nextInt();
            for (int i = 2; i <= a / i; i++) {
                while (a % i == 0) {
                    a /= i;
                    primes.put(i, primes.getOrDefault(i, 0) + 1);
                }
            }
            if (a > 1) primes.put(a, primes.getOrDefault(a, 0) + 1);
        }
        
        long ret = 1; // 约数 1 没有记录在上面
        for (var cnt : primes.values()) ret = ret * (cnt + 1) % MOD;
        System.out.println(ret);
    }
}
```

