[791. 高精度加法](https://www.acwing.com/problem/content/793/)

#### 算法：

*#高精度加法*

**压位**

- 压位就是使用一个更大的进制来存储一个数。

  - 不压位数组里每一个数存0 ~ 9
  
  - 压 9 位就是每个数存0 ~ 999999999，这样数组长度会缩小到九分之一。

- 加法压 9 位，乘法压 4 位。

#### 时间复杂度分析：

O(n)，n 为 A，B 中长度较长的数字的长度。

#### 代码：

##### 不压位

```java
import java.util.*;

class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        String a = sc.next(), b = sc.next();
        List<Integer> A = new ArrayList<>(), B = new ArrayList<>();
        for (int i = a.length() - 1; i >= 0; i--) A.add(a.charAt(i) - '0');
        for (int i = b.length() - 1; i >= 0; i--) B.add(b.charAt(i) - '0');
        
        var C = add(A, B);
        for (int i = C.size() - 1; i >= 0; i--) System.out.print(C.get(i));
    }
    
    static List<Integer> add(List<Integer> A, List<Integer> B) {
        List<Integer> C = new ArrayList<>();
        
        int t = 0; // 进位
        for (int i = 0; i < A.size() || i < B.size() || t != 0; i++) {
            if (i < A.size()) t += A.get(i);
            if (i < B.size()) t += B.get(i);
            C.add(t % 10);
            t /= 10;
        }
        
        return C;
    }
}
```

##### 压位

```java
import java.util.*;

class Main {
    static int base = (int)1e9;
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        String a = sc.next(), b = sc.next();
        List<Integer> A = new ArrayList<>(), B = new ArrayList<>();
        
        // 将 a 和 b 每 9 位放到 A 和 B 中
        for (int i = a.length() - 1, j = 0, s = 0, t = 1; i >= 0; i--) {
            s += (a.charAt(i) - '0') * t; // 当前的和（是从小到大计算的）
            t *= 10;
            j++; // 记录当前压了几位
            if (j == 9 || i == 0) {
                A.add(s);
                s = j = 0; // 重新统计
                t = 1;
            }
        }
        for (int i = b.length() - 1, j = 0, s = 0, t = 1; i >= 0; i--) {
            s += (b.charAt(i) - '0') * t; // 当前的和（是从小到大计算的）
            t *= 10;
            j++; // 记录当前压了几位
            if (j == 9 || i == 0) {
                B.add(s);
                s = j = 0; // 重新统计
                t = 1;
            }
        }
        
        var C = add(A, B);
        System.out.print(C.get(C.size() - 1)); // 第一个数不需要最高位补 0
        for (int i = C.size() - 2; i >= 0; i--) System.out.printf("%09d", C.get(i)); // 其它数不足 9 位要最高位补 0
    }
    
    static List<Integer> add(List<Integer> A, List<Integer> B) {
        List<Integer> C = new ArrayList<>();
        
        int t = 0; // 进位
        for (int i = 0; i < A.size() || i < B.size() || t != 0; i++) {
            if (i < A.size()) t += A.get(i);
            if (i < B.size()) t += B.get(i);
            C.add(t % base); // 压位
            t /= base; // 压位
        }
        
        return C;
    }
}
```

