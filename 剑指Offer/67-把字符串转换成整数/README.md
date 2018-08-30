# 题目描述

将一个字符串转换成一个整数(实现Integer.valueOf(string)的功能，但是string不符合数字要求时返回0)，要求不能使用字符串转换整数的库函数。 数值为0或者字符串不是一个合法的数值则返回0。

## 示例

输入:

```
+2147483647
    1a33
```

输出

```
2147483647
    0
```

## 解题思路

注意处理正负号和非法字符。

## 参考代码

```cpp
class Solution {
public:
    int StrToInt(string str) {
        int num = 0;
        bool neg = false, valid = false;
        int pos = 0;
        while (pos < str.length() && str[pos] == ' ') pos++;  /* 跳过空格 */
        if (str[pos] == '+') {    /* 处理正号 */
            neg = false;  pos++;  valid = true;
        } else if (str[pos] == '-') {    /* 处理负号 */
            neg = true;  pos++;  valid = true;
        } else if (str[pos] >= '0' && str[pos] <= '9') {  /* 没有正负号 */
            valid = true;
        }
        while (valid && pos < str.length()) {
            if (str[pos] < '0' || str[pos] > '9') {    /* 不是数字 */
                valid = false;
                break;
            }
            num *= 10;
            num += str[pos++] - '0';
        }
        return valid ? (neg ? -num : num) : 0;
    }
};
```
