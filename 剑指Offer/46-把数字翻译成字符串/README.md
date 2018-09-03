# 题目描述

给定一个数字，按照如下规则把它翻译为字符串：

- 0 翻译成 "a"
- 1 翻译成 "b"
- ......
- 11 翻译成 "l"
- ......
- 25 翻译成 "z"

一个数可能有多个翻译。请编写一个函数，用来计算一个数字有多少种不同的翻译方法。

## 示例

12258 有 5 种不同的翻译，分别是 "bccfi"、"bwfi"、"bczi"、"mcfi"、"mzi"。

## 解题思路

定义函数 f(i) 表示从第 i 位数字开始的不同翻译的数目，那么 `f(i)=f(i+1)+g(i,i+1)xf(i+2)`。当第 i 位和第 i+1 位两位数字拼接起来的数字在 10~25 的范围内时，函数 `g(i,i+1)` 的值为 1；否则为 0。

从数字的末尾开始，从右到左翻译并计算不同翻译的数目。消除重复的子问题。

## 参考代码

```cpp
class Solution {
public:
    int GetTranslationCount(int number) {
        if (number < 0) return 0;
        return GetTranslationCount(to_string(number));
    }
    int GetTranslationCount(const string& num) {
        int len = num.length();
        int *counts = new int[len];
        int count = 0;
        counts[len - 1] = 1;
        for (int i = len - 2; i >= 0; --i) {
            count = counts[i + 1];
            int n = (num[i] - '0') * 10 + (num[i + 1] - '0');
            if (n >= 10 && n <= 25) {
                if (i < len - 2) count += counts[i + 2];
                else count += 1;
            }
            counts[i] = count;
        }
        count = counts[0];
        delete [] counts;
        return count;
    }
}
```
