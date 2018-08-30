# 题目描述

求1+2+3+...+n，要求不能使用乘除法、for、while、if、else、switch、case等关键字及条件判断语句（A?B:C）。

## 解题思路

- 利用构造函数求解
- 利用虚函数求解
- 利用函数指针求解
- 利用模板类型求解

## 参考代码

递归求解，注意递归结束条件。

```cpp
class Solution {
public:
    int Sum_Solution(int n) {
        int sum = n;
        sum && (sum += Sum_Solution(n-1));
        return sum;
    };
};
```
