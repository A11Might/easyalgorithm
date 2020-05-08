[840. 模拟散列表](https://www.acwing.com/problem/content/842/)

#### 算法：

*#散列表*

#### 时间复杂度分析：



#### 代码：

1. 拉链法

   ```java
   import java.util.*;
   
   class Main {
       static final int N = 100003;
       static int idx;
       static int[] h = new int[N], e = new int[N], ne = new int[N];
       
       static void insert(int x) {
           int k = (x % N + N) % N;
           e[idx] = x;
           ne[idx] = h[k];
           h[k] = idx++;
       }
       
       static boolean find(int x) {
           int k = (x % N + N) % N;
           for (int i = h[k]; i != -1; i = ne[i]) {
               if (e[i] == x) return true;
           }
           return false;
       }
       
       public static void main(String[] args) {
           Scanner sc = new Scanner(System.in);
           int n = sc.nextInt();
           
           Arrays.fill(h, -1);
           while (n-- > 0) {
               String op = sc.next();
               int x = sc.nextInt();
               if (op.equals("I")) insert(x);
               else {
                   if (find(x)) System.out.println("Yes");
                   else System.out.println("No");
               }
           }
       }
   }
   ```

2. 开放寻址法

   ```java
   import java.util.*;
   
   class Main {
       static final int N = 200003, NULL = Integer.MAX_VALUE;
       static int[] h = new int[N];
       
       static int find(int x) {
           int k = (x % N + N) % N;
           while (h[k] != NULL && h[k] != x) {
               k++;
               // 当看到最后一个位置时都没有找到目标元素，则跳到第一个位置继续看
               if (k == N) k = 0;
           }
           return k;
       }
       
       public static void main(String[] args) {
           Scanner sc = new Scanner(System.in);
           int n = sc.nextInt();
           
           Arrays.fill(h, NULL);
           while (n-- > 0) {
               String op = sc.next();
               int x = sc.nextInt();
               if (op.equals("I")) h[find(x)] = x;
               else {
                   if (h[find(x)] == NULL) System.out.println("No");
                   else System.out.println("Yes");
               }
           }
       }
   }
   ```

   

