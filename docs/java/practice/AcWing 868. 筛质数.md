[868. 筛质数](https://www.acwing.com/problem/content/870/)

#### 算法：



#### 时间复杂度分析：



#### 代码：

```java
import java.util.*;

class Main {
    static final int N = 1000010;
    static int n;
    static int cnt;
    static int[] primes = new int[N];
    static boolean[] st = new boolean[N];
    
    static void getPrimes() {
        for (int i = 2; i <= n; i++) {
            if (!st[i]) primes[cnt++] = i;
            for (int j = 0; primes[j] <= n / i; j++) {
                st[primes[j] * i] = true;
                if (i % primes[j] == 0) break;
            }
        }
    }
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        n = sc.nextInt();
        getPrimes();
        System.out.println(cnt);
    }
}
```

