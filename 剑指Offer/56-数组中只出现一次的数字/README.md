# 题目描述

一个整型数组里除了两个数字之外，其他的数字都出现了偶数次。请写程序找出这两个只出现一次的数字。

## 解题思路

将数组中所有数字进行异或（偶数次的数字全部异或结果为0），结果为我们要找的两个数字的异或。
根据这两个数字异或结果中的某一位1可以把原数组分成两部分，两个子数组分别进行异或得到这两个数字。

## 参考代码

```cpp
class Solution {
public:
    void FindNumsAppearOnce(vector<int> data,int* num1,int *num2) {
        int num = accumulate(data.begin(), data.end(), 0, bit_xor<int>());
        num &= -num;    // 找到最右边为1的位
        *num1 = *num2 = 0;
        for (auto &x : data)
            if ((num & x) == 0) *num1 ^= x;
            else *num2 ^= x;
    }
};
```
