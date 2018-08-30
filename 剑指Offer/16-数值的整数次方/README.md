# 题目描述

给定一个double类型的浮点数base和int类型的整数exponent。求base的exponent次方。

## 解题思路

快速幂求解

## 参考代码

```cpp
class Solution {
public:
    double Power(double base, int exponent) {
        if (exponent == 0) return 1;
        if (base == 0) return 0;
        double result = 1.0;
        int n = exponent;
        if (n < 0)
            n = -n;
        while (n) {
            if (n & 1)
                result *= base;
            base *= base;
            n >>= 1;
        }
        return exponent < 0 ? 1.0/result : result;
    }
};
```
