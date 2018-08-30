# 题目描述

请实现一个函数用来判断字符串是否表示数值（包括整数和小数）。例如，字符串"+100","5e2","-123","3.1416"和"-1E-16"都表示数值。 但是"12e","1a3.14","1.2.3","+-5"和"12e+4.3"都不是。

## 解题思路

注意处理各种情况。

- 小数可以没有整数部分：`.123 = 0.123`
- 小数点后面可以没有数字：`233. = 233.0`
- 当 `e` 或 `E` 前面没有数字时，不能表示字符串：`.e1、e1`
- 当 `e` 或 `E` 后面没有数字时，不能表示字符串：`12e`

## 参考代码

```cpp
class Solution {
public:
    bool isNumeric(char* string)
    {
        if (string == nullptr || *string == '\0') return false;
        bool isnumeric = false;
        if (*string == '+' || *string == '-') string++;    /* 正负号可有可无 */
        while (*string >= '0' && *string <= '9') {    /* 扫描数字 */
            isnumeric = true;
            string++;
        }
        if (*string == '.') string++;    /* 小数点可有可无 */
        while (*string >= '0' && *string <= '9') {    /* 小数点后面数字 */
            isnumeric = true;
            string++;
        }
        if (isnumeric && (*string == 'e' || *string == 'E')) {  /* 有指数 */
            string++;
            isnumeric = false;    /* 准备判断指数部分 */
            if (*string == '+' || *string == '-') string++; /* 正负号可有可无 */
            while (*string >= '0' && *string <= '9') {    /* 扫描数字 */
                isnumeric = true;
                string++;
            }
        }
        return isnumeric && *string == '\0';    /* 处理完成应到字符串末尾 */
    }

};
```
