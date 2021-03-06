[1068. 环形石子合并](https://www.acwing.com/problem/content/1070/)

#### 算法：

*DP* *区间 DP*

**简化问题**

关键，看作一个环，实际是进行连边操作，看能够连多少边。

直接枚举最后一步的缺口在哪里，然后拉开转化为链式问题。
> 实际上就是枚举，但是这种枚举破开的方式，关键是怎么看待其实每个边的地位都一样这件事
> n^4
> 本质是什么？本质是求n个长度为n的链
> 将环形链复制在后面，复制一遍，实际就是对2n的链上做. 牛逼！！
> 非常巧妙！！2n^3

**Tips**

区间 dp 问题代码实现方式有两种

- 迭代式：当区间只有一维的时候，迭代式较好写

  ```java
  for (int len = 1; len <= n; len++) { // 循环区间长度
      for (int L = 1; L + len - 1 <= n; L++) { // 循环右端点
          R = L + len - 1; // 求出右端点
      }
  }
  ```

  

- 记忆化搜索

#### 时间复杂度分析：



#### 代码：

```java

```

