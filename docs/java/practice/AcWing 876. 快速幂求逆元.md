[876. 快速幂求逆元](https://www.acwing.com/problem/content/878/)

#### 算法：

*#快速幂*

##### 乘法逆元的定义

> 若整数 b，m 互质，并且对于任意的整数 a，如果满足 b|a，则存在一个整数 x，使得 a / b ≡ a ∗ x (mod m)，则称 x 为 b 的模 m 乘法逆元，记为 b<sup>−1</sup>(mod m)。
> b 存在乘法逆元的充要条件是 b 与模数 m 互质。当模数 m 为质数时，b<sup>m−2</sup> 即为 b 的乘法逆元。

给定一个 b，使得 b * x ≡ 1(mod p)，x 就是 b mod p 的逆元，其中 p 是质数， b 和 p 是互质的，由费马小定理 b<sup>p - 1</sup> ≡ 1(mod p) 得 b * b<sup>p - 2</sup> ≡ 1(mod p)，所以 x = b<sup>p - 2</sup>。

当 b 和 p 不互质时，b 是 p 的倍数，b * x 也是 p 的倍数，mod p 一定等于 0，不可能余 1，所以不存在逆元。

#### 时间复杂度分析：



#### 代码：

