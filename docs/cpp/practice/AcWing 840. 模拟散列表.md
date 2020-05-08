[840. 模拟散列表](https://www.acwing.com/problem/content/842/)

#### 算法：

*#散列表*

#### 时间复杂度分析：



#### 代码：

1. 拉链法

   ```cpp
   #include <bits/stdc++.h>
   
   using namespace std;
   
   const int N = 100003;
   
   int h[N], e[N], ne[N], idx;
   
   void insert(int x) {
       int t = (x % N + N) % N;
       e[idx] = x;
       ne[idx] = h[t];
       h[t] = idx++;
   }
   
   bool find(int x) {
       int t = (x % N + N) % N;
       for (int i = h[t]; ~i; i = ne[i]) {
           if (e[i] == x) return true;
       }
       return false;
   }
   
   int main() {
       int n;
       cin >> n;
       
       memset(h, -1, sizeof h);
       
       while (n--) {
           char op;
           int x;
           cin >> op >> x;
           if (op == 'I') insert(x);
           else {
               if (find(x)) puts("Yes");
               else puts("No");
           }
       }
       
       return 0;
   }
   ```

2. 开放寻址法

   ```cpp
   #include <bits/stdc++.h>
   
   using namespace std;
   
   const int N = 200003, null = 0x3f3f3f3f;
   
   int h[N];
   
   int find(int x) {
       int t = (x % N + N) % N;
       while (h[t] != null && h[t] != x) {
           t++;
           // 当看到最后一个位置时都没有找到目标元素，则跳到第一个位置继续看
           if (t == N) t = 0;
       }
       return t;
   }
   
   int main() {
       int n;
       cin >> n;
       
       memset(h, 0x3f, sizeof h);
       
       while (n--) {
           char op;
           int x;
           cin >> op >> x;
           int k = find(x);
           if (op == 'I') h[k] = x;
           else {
               if (h[k] == null) puts("No");
               else puts("Yes");
           }
       } 
       
       return 0;
   }
   ```

   

