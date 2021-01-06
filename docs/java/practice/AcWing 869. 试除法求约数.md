[869. 试除法求约数](https://www.acwing.com/problem/content/871/)

#### 算法：



#### 时间复杂度分析：



#### 代码：

```java
import java.util.*;

class Main {
    static List<Integer> getDivisors(int x) {
        List<Integer> ret = new ArrayList<>();
        for (int i = 1; i <= x / i; i++) {
            if (x % i == 0) {
                ret.add(i);
                if (i != x / i) ret.add(x / i);
            }
        }
        
        ret.sort((o1, o2) -> o1 - o2);
        return ret;
    }
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        while (n-- > 0) {
            int a = sc.nextInt();
            for (int num : getDivisors(a)) {
                System.out.print(num + " ");
            }
            System.out.println();
        }
    }
}
```

