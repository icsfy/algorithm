# 题目描述

输入一个整数，输出该数二进制表示中1的个数。其中负数用补码表示。

## 解题思路

`x & (x-1)` 可将 `x` 中的最右边一位 `1` 置为 `0`。

## 参考代码

```cpp
class Solution {
public:
     int  NumberOf1(int n) {
         int cnt = 0;
         while (n) {
             n = n & (n - 1);
             cnt++;
         }
         return cnt;
     }
};
```
