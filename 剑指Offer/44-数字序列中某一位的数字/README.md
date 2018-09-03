# 题目描述

数字以 `0123456789101112131415...` 的格式序列化到一个字符序列中。在这个序列中，第 5 位（从 0 开始计数）是 5，第 13 位是 1，第 19 位是 4，等等。请写一个函数，求任意第 n 位对应的数字。

## 解题思路

一位数有 10 个(0~9)，两位数有 90 个(10~99)，三位数有 900 个(100~999)...

## 参考代码

```cpp
class Solution {
public:
    int digitAtIndex(int index) {
        if (index < 0) return 0;
        int digits = 1;
        int num = countOfIntegers(digits);
        while (index > num * digits) {
            index -= digits * num;
            num = countOfIntegers(++digits);
        }
        return digitAtIndex(index, digits);
    }

    int countOfIntegers(int digits) {
        if (digits == 1)  return 10;
        return 9 * pow(10, digits - 1);
    }

    int digitAtIndex(int index, int digits) {
        int num = beginNumber(digits) + index / digits;
        int indexFromRight = digits - index % digits;
        while (--indexFromRight) num /= 10;
        return num % 10;
    }

    int beginNumber(int digits) {
        return digits == 1 ? 0 : pow(10, digits - 1);
    }
}
```
