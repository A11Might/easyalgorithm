[867. 分解质因数](https://www.acwing.com/problem/content/869/)

#### 算法：



#### 时间复杂度分析：



#### 代码：

```java
import java.util.*;

class Main {
    static void divide(int x) {
        for (int i = 2; i <= x / i; i++) {
            if (x % i == 0) {
                int cnt = 0;
                while (x % i == 0) {
                    x /= i;
                    cnt++;
                }
                System.out.println(i + " " + cnt);
            }
        }
        if (x > 1) System.out.println(x + " " + 1);
    }
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        while (n-- > 0) {
            int a = sc.nextInt();
            divide(a);
            System.out.println();
        }
    }
}
```

