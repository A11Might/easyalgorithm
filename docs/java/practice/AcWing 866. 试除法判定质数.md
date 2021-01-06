[866. 试除法判定质数](https://www.acwing.com/problem/content/868/)

#### 算法：



#### 时间复杂度分析：



#### 代码：

```java
import java.util.*;
import java.io.*;

class Main {
    static boolean isPrime(int x) {
        if (x < 2) return false;
        for (int i = 2; i <= x / i; i++) {
            if (x % i == 0) return false;
        }
        return true;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        while (n-- > 0) {
            int a = sc.nextInt();
            if (isPrime(a)) System.out.println("Yes");
            else System.out.println("No");
        }
    }
}
```

