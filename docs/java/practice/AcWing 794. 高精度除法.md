[794. 高精度除法](https://www.acwing.com/problem/content/796/)

#### 算法：

*#高精度除法*

#### 时间复杂度分析：

O(n)，n 为数字 A 的长度。

#### 代码：

```java
import java.util.*;

class Main {
    static int div(List<Integer> A, int b, List<Integer> C) {
        int t = 0; // 余数
        for (int i = A.size() - 1; i >= 0; i--) {
            t = t * 10 + A.get(i);
            C.add(t / b);
            t %= b;
        }
        
        // 去除前导 0
        while (C.size() > 1 && C.get(0) == 0) C.remove(0);
        return t; // 返回余数
    }
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        String a = sc.nextLine();
        List<Integer> A = new ArrayList<>();
        for (int i = a.length() - 1; i >= 0; i--) A.add(a.charAt(i) - '0');
        int b = sc.nextInt();
        
        List<Integer> C = new ArrayList<>();
        int remainder = div(A, b, C);
        // 除法是从高位向低位计算的
        for (int i = 0; i < C.size(); i++) System.out.print(C.get(i));
        System.out.println();
        System.out.print(remaind);
    }
}
```

