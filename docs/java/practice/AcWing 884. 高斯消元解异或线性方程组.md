[884. 高斯消元解异或线性方程组](https://www.acwing.com/problem/content/886/)

#### 算法：

*#高斯消元*

- 类似高斯消元，将方程组消成上三角矩阵

  枚举每一列

  1. 找到当前列中元素非零的行
  2. 将该非零行交换到最上面
  3. 使用非零行将下面所有行的该列位置消成零

- 判断

  - 完美上三角矩阵 - 唯一解
  - 有矛盾 - 无解
  - 无矛盾 - 无穷多解

#### 时间复杂度分析：



#### 代码：

