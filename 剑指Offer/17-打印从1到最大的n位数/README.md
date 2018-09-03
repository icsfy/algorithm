# 题目描述

输入数字 n，按顺序打印从 1 到最大的 n 位十进制数。

## 示例

输入 3，则打印出 1、2、3 一直到最大的 3 位数 999。

## 解题思路

n 位所有十进制数其实就是 n 个从 0 到 9 的全排列。

## 参考代码

```cpp
class Solution {
public:
    void Print1ToMaxOfNDigits(int n) {
        if (n < 0) return;
        char *num = new char[n + 1];
        num[n] = '\0';
        for (int i = 0; i < 10; ++i) {
            num[0] = i + '0';
            Print1ToMaxOfNDigitsRecursively(num, n, 0);
        }
        delete [] num;
    }

    void Print1ToMaxOfNDigitsRecursively(char *num, int len, int index) {
        if (index == len - 1) {
            PrintNumber(num);
            return;
        }
        for (int i = 0; i < 10; ++i) {
            num[index + 1] = i + '0';
            Print1ToMaxOfNDigitsRecursively(num, len, index + 1);
        }
    }

    void PrintNumber(char *num) {
        while (*num == '0') num++;
        printf("%s\t", num);
    }
}
```
