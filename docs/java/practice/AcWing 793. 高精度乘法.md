[793. 高精度乘法](https://www.acwing.com/problem/content/795/)

#### 算法：

*#高精度乘法*

#### 时间复杂度分析：

O(n)，n 为数字 A 的长度。

#### 代码：

```java
import java.util.*;

class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        String a = sc.next();
        int b = sc.nextInt();
        List<Integer> A = new ArrayList<>();
        for (int i = a.length() - 1; i >= 0; i--) A.add(a.charAt(i) - '0');
        
        if (b == 0) System.out.println("0");
        else {
            var C = mul(A, b);
            for (int i = C.size() - 1; i >= 0; i--) System.out.print(C.get(i));
        }
    }
    
    static List<Integer> mul(List<Integer> A, int b) {
        List<Integer> C = new ArrayList<>();
        
        int t = 0; // 进位
        for (int i = 0; i < A.size(); i++) {
            t += A.get(i) * b;
            C.add(t % 10);
            t /= 10;
        }
        if (t != 0) C.add(t);
        
        return C;
    }
}
```

