[1072. 树的最长路径](https://www.acwing.com/problem/content/1074/)

#### 算法：

*DP* *树形 DP*

当树没有权重的时候，找树的直径：

1. 任取一个点作为起点，找到距离该点最远的一个点 u。dfs、bfs 都可以

2. 再找到距离 u 最远的一点 v。dfs，bfs 都可以

那么 u 和 v 之间的路径就是一条直径

https://www.acwing.com/solution/content/12577/



无向图所以任意选择一个点作为根节点，然后将所有直径分类：在每条直径上找到一个高度最高的点，将这个路径放到这个点所在集合中，这样按每个点将直径分类后找到每一类中的最大值，取一个max。

当我们固定完一个点 u 后，如何求出高度最高的点是 u 的所有路径中的最大值？

首先找到节点 u 的所有子节点向下的最大长度求出来，前两大加起来就是最大值，可以使用树形 DP。

注意：如果将向下长度初始化为 0，可以不考虑其是负数的情况。

#### 时间复杂度分析：



#### 代码：

```java

```

