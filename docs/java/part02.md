# 数据结构

链表、栈与队列、单调队列、单调栈、kmp、Trie、并查集、堆、Hash 表。

---

#### 单链表

数组模拟单链表

每个单链表节点有两个属性：这个节点的值和下一个节点的指针。使用整型数组 e 存储节点的值，整型数组 ne 存储节点的 next 指针，使用下标将 e 和 ne 关联起来。

注：head 存储的是链表的第一个节点。

```java
// head 存储链表头，数组 e 存储节点的值，数组 ne 存储节点的 next 指针，idx 表示当前用到了哪个节点
int head, idx;
int[] e, ne;

// 初始化
void init() {
	head = -1;
    idx = 0;
}

// 在链表头插入一个数 a
void insert(int a) {
    e[idx] = a;
    ne[idx] = head;
    head = idx++;
}

// 将头结点删除，需要保证头结点存在
void remove() {
    head = ne[head];
}
```

#### 双链表

数组模拟双链表

每个双链表节点有三个属性：这个节点的值、上一个节点的指针和下一个节点的指针。使用整型数组 e 存储节点的值，整型数组 l 存储节点的 pre 指针，整型数组 r 存储节点的 next 指针，使用下标将 e 和 l,r 关联起来。

注：与单链表的 head 不同的是，双链表中的左端点 0 和右端点 1 是虚拟节点，并不是真实链表中的一部分。

```java
// 数组 e 表示节点的值，数组 l 表示节点的左指针，数组 r 表示节点的右指针，idx表示当前用到了哪个节点
int idx;
int[] e, l, r;

// 初始化
void init() {
    // 0 是左端点，1 是右端点
    r[0] = 1;
    l[1] = 0;
    idx = 2;
}

// 在节点 a 的右边插入一个数 x
void insert(int a, int x) {
    e[idx] = x;
    l[idx] = a;
    r[idx] = r[a];
    l[r[a]] = idx;
    r[a] = idx++;
}

// 删除节点 a
void remove(int a) {
    l[r[a]] = l[a];
    r[l[a]] = r[a];
}
```

#### 栈

先进后出

```java
// tt 表示栈顶
int tt = 0;
int[] stk;

// 向栈顶插入一个数
stk[++tt] = x;

// 从栈顶弹出一个数
tt-- ;

// 栈顶的值
stk[tt];

// 判断栈是否为空
if (tt > 0) not empty;
else empty;
```

#### 队列

先进先出

1. 普通队列

   队列中的元素个数：hh - tt。

   ```java
   // hh 表示队头，tt 表示队尾
   int hh = 0, tt = -1;
   int[] q;
   
   // 向队尾插入一个数
   q[++tt] = x;
   
   // 从队头弹出一个数
   hh++ ;
   
   // 队头的值
   q[hh];
   
   // 判断队列是否为空
   if (hh <= tt) not empty;
   else empty;
   ```

2. 循环队列

   队列中的元素个数：如果 tt > hh，个数就是tt - hh；如果 hh == tt，个数是 0；如果 hh > tt，个数就是 tt + n - hh，n 是队列数组的长度。

   ```java
   // hh 表示队头，tt 表示队尾的后一个位置
   int hh = 0, tt = 0;
   int[] q;
   
   // 向队尾插入一个数
   q[tt++] = x;
   if (tt == N) tt = 0;
   
   // 从队头弹出一个数
   hh++;
   if (hh == N) hh = 0;
   
   // 队头的值
   q[hh];
   
   // 判断队列是否为空
   if (hh != tt) not empty;
   else empty;
   ```

#### 单调栈

常见模型：找出每个数左边离它最近的比它大/小的数。

```java
int tt = 0;
for (int i = 1; i <= n; i++ ) {
    while (tt && check(stk[tt], i)) tt-- ;
    stk[++tt] = i;
}
```

#### 单调队列

常见模型：找出滑动窗口中的最大值/最小值。

```java
int hh = 0, tt = -1;
for (int i = 0; i < n; i++ ) {
    while (hh <= tt && check_out(q[hh])) hh++ ;  // 判断队头是否滑出窗口
    while (hh <= tt && check(q[tt], i)) tt-- ;
    q[++tt] = i;
}
```

#### KMP

注意：

- s 和 p 的下标是从 1 开始的。

- next[i] 的定义是非平凡的最大后缀等于最大前缀，即必须要小于 i，所以 next[1]必须等于 0，i 就只能从 2 开始循环了。

```java
// 数组 s 是长文本，数组 p 是模式串，n 是 s 的长度，m 是 p 的长度
// 求模式串的 Next 数组：
for (int i = 2, j = 0; i <= m; i++) {
    while (j != 0 && p[i] != p[j + 1]) j = ne[j];
    if (p[i] == p[j + 1]) j++ ;
    ne[i] = j;
}

// 匹配
for (int i = 1, j = 0; i <= n; i++) {
    while (j != 0 && s[i] != p[j + 1]) j = ne[j];
    if (s[i] == p[j + 1]) j++ ;
    if (j == m) {
        j = ne[j];
        // 匹配成功后的逻辑
    }
}
```

#### Trie 树

用来高效地存储和查找字符串集合的数据结构。

```java
// 二维数组 son 存储树中每个节点的子节点，数组 cnt存储以每个节点结尾的单词数量
// idx 表示当前用到了第几个节点
// 0 号点既是根节点，又是空节点
int idx;
int[] cnt;
int[][] son;

// 插入一个字符串
void insert(char[] str) {
    int p = 0; // 从根结点开始
    for (int i = 0; str[i]; i++) {
        int u = str[i] - 'a';
        if (son[p][u] == 0) son[p][u] = ++idx;
        p = son[p][u];
    }
    cnt[p]++ ;
}

// 查询字符串出现的次数
int query(char[] str) {
    int p = 0; // 从根结点开始
    for (int i = 0; i < str.length; i++) {
        int u = str[i] - 'a';
        if (son[p][u] == 0) return 0;
        p = son[p][u];
    }
    return cnt[p];
}
```

#### 并查集

用处：用来高效的将两个集合合并或者询问两个元素是否在一个集合当中的数据结构。操作的时间复杂度近乎 O(1)。

基本原理：每个集合用一棵树来表示。树根的编号就是整个集合的编号。每个节点存储它的父节点，p[x] 表示 x 的父节点。

- 如何判断树根：if (p[i] == i) 则 i 为树根。
- 如何求 x 的集合编号：while (p[i] != i) i = p[i]；。
- 如何合并两个集合：x 是一个集合的编号，y 是另一个集合的编号，p[x] = y。

优化 - 路径压缩：查到树根 x（集合编号）后，将查找路径上的点 i 直接连到树根上 p[i] = x。

1. 朴素并查集

   ```java
   int[] p; // 存储每个点的父亲节点
   
   // 返回 x 的祖宗节点 + 路径压缩
   int find(int x) {
       if (p[x] != x) p[x] = find(p[x]);
       return p[x];
   }
   
   // 初始化，假定节点编号是 1 ~ n
   for (int i = 1; i <= n; i++) p[i] = i;
   
   // 合并 a 和 b 所在的两个集合：
   p[find(a)] = find(b);
   ```

2. 维护 size 的并查集

   ```java
   // 数组 p 存储每个点的父亲节点, 数组 size 只有祖宗节点的有意义，表示祖宗节点所在集合中的点的数量
   int[] p, size;
   
   // 返回 x 的祖宗节点
   int find(int x) {
       if (p[x] != x) p[x] = find(p[x]);
       return p[x];
   }
   
   // 初始化，假定节点编号是 1 ~ n
   for (int i = 1; i <= n; i ++ ) {
       p[i] = i;
       size[i] = 1;
   }
   
   // 合并 a 和 b 所在的两个集合：
   size[find(b)] += size[find(a)];
   p[find(a)] = find(b);
   ```

3. 维护到祖宗节点距离的并查集

   ```java
   // 数组 p 存储每个点的父亲节点, d[x] 存储 x 到 p[x] 的距离
   int[] p, d;
   
   // 返回 x 的祖宗节点
   int find(int x) {
       if (p[x] != x) {
           int u = find(p[x]);
           d[x] += d[p[x]];
           p[x] = u;
       }
       return p[x];
   }
   
   // 初始化，假定节点编号是 1  ~ n
   for (int i = 1; i <= n; i++) {
       p[i] = i;
       d[i] = 0;
   }
   
   // 合并 a 和 b 所在的两个集合：
   p[find(a)] = find(b);
   d[find(a)] = distance; // 根据具体问题，初始化 find(a) 的偏移量
   ```

#### 堆

- 小根堆的递归定义：根节点的值小于等于左右两个子节点，也就是根节点是堆中的最小值。

  大根堆的递归定义：同理。

- 支持的操作（下标从 1 开始）：

  - 插入一个数：在堆的最后一个位置插入一个元素，然后从这个元素开始向上堆化。

    heap[++size] = x; up(size);

  - 求集合中的最小值：第一个数一定是最小值。

    heap[q];

  - 删除最小值：将堆的最后一个元素与第一个元素交换，然后删除最后一个元素（因为删除数组中的最后一个元素比较容易实现），从堆顶开始向下堆化。

    heap[1] = heap[size]; size--; down(1);

  - 删除任意一个元素：同上类似，不同的是如果 heap[k] 的值变大了，则需要向下堆化；如果 heap[k] 的值变小了，则需要向上堆化。我们可以直接同时执行 down(k); up(k);，由于只会出现一种情况，所以它们中只有一个会被执行。

    heap[k] = heap[size]; size--; down(k); up(k);

  - 修改任意一个元素：同上。

    heap[k] = x; down(k); up(k);

- 建堆的时间复杂度为 O(n)：

  最后一层的节点个数同剩余节点个数相同为 n / 2。

  倒数第二层的节点个数为 n / 4，向下堆化最多移动一层。倒数第三层的节点个数为 n / 8，向下堆化最多移动两层。依次类推，可以得到 s = n / 4 * 1 + n / 8 * 2 + n / 16 * 3 + ... = n * (1 / 4 + 2 / 8 + 3 / 16 + ...)。

  ​			2 * s = n * (1 / 2 + 2 / 4 + 3 / 8 + ...)

  减去           s = n * (           1 / 4 + 2 / 8 + 3 / 16 + ...)

  等于           s = n * (1 / 2 + 1 / 4 + 1 / 8 + ...)

  其中 1 / 2 + 1 / 4 + 1 / 8 + ... < 1，所以建堆的时间复杂度为 O(n)。

- ph 数组和 hp 数组（修改或删除堆中中间节点的时候会用到）：

  使用 position 表示在堆外的位置，也就是第几个插入的，用 heap 表示在堆中的位置，所以 ph 表示的就是 position -> heap 相当于求出当前点对应到堆中的位置，hp 表示 heap -> position，相当于求出堆中点对应到 position 中的位置。

  也就是 ph[i] == x：第 i 个插入的元素是 x；hp[x] == i：元素 x 是第 i 个插入的。 

  当前堆中元素 x 和 y 发生交换后，ph 和 hp 中对应的两个元素也需要交换。

```java
// 数组 h 存储堆中的值, h[1] 是堆顶，x 的左儿子是 2x, 右儿子是 2x + 1
// ph[k] 存储第 k 个插入的点在堆中的位置
// hp[k] 存储堆中下标是 k 的点是第几个插入的
int size;
int[] h, ph, hp;

// 交换两个点，及其映射关系
void heapSwap(int a, int b) {
    swap(ph, hp[a], hp[b]);
    swap(hp, a, b);
    swap(h, a, b);
}

void down(int u) {
    int t = u;
    if (u * 2 <= size && h[u * 2] < h[t]) t = u * 2;
    if (u * 2 + 1 <= size && h[u * 2 + 1] < h[t]) t = u * 2 + 1;
    if (u != t) {
        heapSwap(u, t);
        down(t);
    }
}

void up(int u) {
    while (u / 2 > 0 && h[u] < h[u / 2]) {
        heapSwap(u, u / 2);
        u >>= 1;
    }
}

// O(n) 建堆
for (int i = n / 2; i > 0; i-- ) down(i);
```

#### 一般哈希

哈希函数：f(x) = (x % N + N) % N，其中 +N %N 是为了让 k 为正值，因为当 x 为负数时，%N 的结果也为负数。取模的数 N 是质数，冲突的概率会低一些，如果 N 是合数，比如是 2 的倍数，那么所有被 2 整除的数就不会被分到奇数位置上，分散的程度会变低，冲突概率就会变大。

1. 拉链法

   ```java
   int idx;
   int[] h, e, ne;
   
   // 向哈希表中插入一个数
   void insert(int x) {
       int k = (x % N + N) % N;
       e[idx] = x;
       ne[idx] = h[k];
       h[k] = idx ++ ;
   }
   
   // 在哈希表中查询某个数是否存在
   bool find(int x) {
       int k = (x % N + N) % N;
       for (int i = h[k]; i != -1; i = ne[i]) {
           if (e[i] == x) return true;
       }
       return false;
   }
   ```

2. 开放寻址法

   注：数组大小经验值是开到题目给定范围的 2 ~ 3 倍，开到这个范围哈希冲突比较低。

   ```java
   int NULL = Integer.MAX_VALUE;
   int[] h;
   
   // 如果 x 在哈希表中，返回 x 的下标；如果 x 不在哈希表中，返回 x 应该插入的位置
   int find(int x) {
       int t = (x % N + N) % N;
       while (h[t] != NULL && h[t] != x) {
           t ++ ;
           if (t == N) t = 0;
       }
       return t;
   }
   ```

#### 字符串哈希

- 用处：快速判断两个字符串是否相等。

- 字符串前缀哈希法（字符串下标从 1 开始）

  h[k] 存储字符串前 k 个字母的哈希值。

- 如何定义前缀的哈希值

  将字符串看成 P 进制的数（左边是高位，右边是低位），每一位上字符的 asc 码表示 P 进制每一位的数字。

  比如：ABCD = (1234)<sub>p</sub> = 1 * p<sup>3</sup> + 2 * p<sup>2</sup> + 3 * p<sup>1</sup> + 4 * p<sup>0</sup>，这样就可以将字符串转化为数字，由于这个数字可能很大所以需要对一个较小 q 的数取模，映射到 0 ~ q - 1。

  注意：

  - 不能将字符映射成 0。假设将字符 A 映射成 0，A 和 AA 转化的数字就都是 0 了。
  - 不考虑冲突情况。当 p == 131 或者 13331，q = 2<sup>64</sup> 时，冲突概率极低。

- 如何求前缀的哈希值

  h[i] = h[i - 1] * p + str[i];

- 如何求子串 str[L, R] 的哈希值

  已知 h[L - 1] 和 h[R]，其中 h[L - 1] = p<sup>L - 2</sup> * ... * p<sup>0</sup>，h[R] = p<sup>R - 1</sup> * ... * p<sup>0</sup>。

  1. 将 h[L - 1] 向左移，使其与 h[R] 对齐：h[L - 1] * p<sup>R - L + 1</sup>。
  2. h[R] - h[L - 1] * p<sup>R - L + 1</sup> 就是子串 str[L, R] 的哈希值。

- 技巧：取模的数用 2<sup>64</sup>，这样直接用 unsigned long long 存储，溢出的结果就是取模的结果。

  但是，Java 中没有无符号类型，所以取模的数用 2<sup>63</sup> - 1（Integer.MAX_VALUE）显式取模，并使用 long 存储取模后的结果。

```java
long mod = Integer.MAX_VALUE;
long[] h, p; // h[k]存储字符串前k个字母的哈希值, p[k]存储 P ^ k mod 2 ^ 64

// 初始化
p[0] = 1;
for (int i = 1; i <= n; i ++ ) {
    h[i] = (h[i - 1] * P + str[i]) % mod;
    p[i] = p[i - 1] * P;
}

// 计算子串 str[l ~ r] 的哈希值
long get(int l, int r) {
    return h[r] - h[l - 1] * p[r - l + 1];
}
```