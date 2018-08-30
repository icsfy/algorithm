# 题目描述

给定一个数组 `A[0,1,...,n-1]`, 请构建一个数组 `B[0,1,...,n-1]`, 其中 B 中的元素 `B[i]=A[0]*A[1]*...*A[i-1]*A[i+1]*...*A[n-1]`。不能使用除法。

## 解题思路

将 `B[i]=A[0]*A[1]*...*A[i-1]*A[i+1]*...*A[n-1]` 看成 `A[0]*A[1]*...*A[i-1]` 和 `A[i+1]*...*A[n-1]` 两部分的乘积。

定义 `C[i]=A[0]*A[1]*...*A[i-1]`，`D[i]=A[i+1]*...*A[n-1]`，
`C[i]` 可以由自上而下的顺序计算出来，`C[i]=C[i-1]*A[i-1]`，
`D[i]` 可以由自下而上的顺序计算出来，`D[i]=D[i+1]*A[i+1]`。

## 参考代码

```cpp
class Solution {
public:
    vector<int> multiply(const vector<int>& A) {
        int len = A.size();
        if (len < 2) return vector<int>();
        vector<int> B(len);
        B[0] = 1;
        for (int i = 1; i < len; ++i)
            B[i] = B[i-1] * A[i-1];
        int temp = 1;
        for (int i = len - 1; i > 0; --i) {
            temp *= A[i];
            B[i-1] = B[i-1] * temp;
        }
        return B;
    }
};
```
