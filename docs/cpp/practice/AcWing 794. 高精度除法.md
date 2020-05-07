[794. 高精度除法](https://www.acwing.com/problem/content/796/)

#### 算法：

*#高精度除法*

#### 时间复杂度分析：

O(n)，n 为数字 A 的长度。

#### 代码：

```cpp
#include <bits/stdc++.h>

using namespace std;

vector<int> div(vector<int> A, int b, int &r) {
    vector<int> C;
    
    for (int i = A.size() - 1; i >= 0; i--) {
        r = r * 10 + A[i];
        C.push_back(r / b);
        r %= b;
    }
    
    // 去除前导 0
    reverse(C.begin(), C.end());
    while (C.size() > 1 && C.back() == 0) C.pop_back();
    
    return C;
}

int main() {
    string a;
    int b;
    cin >> a >> b;
    
    vector<int> A;
    for (int i = a.size() - 1; i >= 0; i--) A.push_back(a[i] - '0');
    
    int r = 0; // 余数
    auto C = div(A, b, r);
    for (int i = C.size() - 1; i >= 0; i--) cout << C[i];
    cout << endl << r << endl;
    
    return 0;
}
```

