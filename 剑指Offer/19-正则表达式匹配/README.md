# 题目描述

请实现一个函数用来匹配包括'.'和'*'的正则表达式。模式中的字符'.'表示任意一个字符，而'*'表示它前面的字符可以出现任意次（包含0次）。 在本题中，匹配是指字符串的所有字符匹配整个模式。例如，字符串"aaa"与模式"a.a"和"ab*ac*a"匹配，但是与"aa.a"和"ab*a"均不匹配

## 解题思路

模式中的第二个字符不是 `'*'`:

- 字符串中的第一个字符和模式中的第一个字符匹配，在字符串和模式上都向后移动一个字符，然后匹配剩余的字符串和模式。
- 字符串中的第一个字符和模式中的第一个字符不匹配，直接返回 `false`。

模式中的第二个字符是 `'*'` 时，有多种不同匹配方式:

- 在模式上向后移动两个字符（`'*'` 和它前面的字符被忽略）
- 模式中的第一个字符和字符串中的第一个字符相匹配，则在字符串上向后移动一个字符，而在模式上有两种选择：
  - 在模式上向后移动两个字符
  - 保持模式不变

## 参考代码

```cpp
class Solution {
public:
    bool match(char* str, char* pattern)
    {
        if (str == nullptr || pattern == nullptr)
            return false;
        return matchCore(str, pattern);
    }

    bool matchCore(char *str, char *pattern)
    {
        if (*str == '\0' && *pattern == '\0')
            return true;
        if (*str != '\0' && *pattern == '\0')
            return false;
        if (*(pattern + 1) == '*')
        {
            if (*pattern == *str || (*pattern == '.' && *str != '\0'))
                return matchCore(str + 1, pattern + 2)
                        || matchCore(str + 1, pattern)
                        || matchCore(str, pattern + 2);
            else
                return matchCore(str, pattern + 2);
        }
        if (*str == *pattern || (*pattern == '.' && *str != '\0'))
            return matchCore(str + 1, pattern + 1);
        return false;
    }
};
```
