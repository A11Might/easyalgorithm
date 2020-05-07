[788. 逆序对的数量](https://www.acwing.com/problem/content/790/)

#### 算法：

*#归并排序*

我们假设归并排序函数可以将区间排好序的同时返回区间内部的逆序对数。

整个区间逆序对可以分为三类：

1. 左半边内部的逆序对数量：mergeSort(L, mid)。

2. 右半边内部的逆序对数量：mergeSort(mid + 1, r)。

3. 两个数分别在左右两边的逆序对数量：统计以右半部分元素作为数对元素的逆序对的个数之和。

   对于两个有序序列 a，b，当 a 中当前元素 A 大于 b 中当前元素 B 时，由于 a 序列是有序的，所以 a 序列中的剩余元素都大于 B，这样得到所有以 B 结尾的逆序对（两个数分别在两边的逆序对），以此类推，求所有以右半部分元素作为数对元素的逆序对的个数之和。

#### 时间复杂度分析：

等于归并排序的时间复杂度 O(n * logn)。

#### 代码：

```cpp
#include <bits/stdc++.h>

using namespace std;

const int N = 100010;

int q[N], cpy[N];

int ms(int q[], int l, int r) {
    if (l >= r) return 0;
    
    int ret = 0, mid = l + r >> 1;
    ret = ms(q, l, mid) + ms(q, mid + 1, r);
    
    int i = l, j = mid + 1, k = l;
    while (i <= mid && j <= r) {
        if (q[i] <= q[j]) cpy[k++] = q[i++];
        else {
            ret += mid - i + 1;
            cpy[k++] = q[j++];
        }
    }
    
    while (i <= mid) cpy[k++] = q[i++];
    while (j <= r) cpy[k++] = q[j++];
    
    for (i = l; i <= r; i++) q[i] = cpy[i];
    
    return ret;
}

int main() {
    int n;
    cin >> n;
    for (int i = 0; i < n; i++) scanf("%d", &q[i]);
    
    cout << ms(q, 0, n - 1) << endl;
    
    return 0;
}
```

