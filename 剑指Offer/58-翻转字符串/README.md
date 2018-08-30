# 题目描述

输入一个英文句子，翻转句子中单词的顺序，但单词内的顺序不变。

## 示例

输入：字符串 `"I am a student."`

输出：`"student. a am I"`

## 解题思路

第一步翻转句子中所有的字符，第二步再翻转每个单词中字符的顺序。

## 参考代码

```cpp
class Solution {
public:
    string ReverseSentence(string str) {
        string res(str);
        reverse(res.begin(), res.end());
        for (int i = 0, start = 0; i <= res.length(); ++i) {
            if (res[i] == ' ' || res[i] == '\0') {
                reverse(&res[start], &res[i]);
                start = i + 1;
            }
        }
        return res;
    }
};
```

## 相关问题

1. 字符串的左旋转操作是把字符串前面的若干个字符转移到字符串的尾部。请定义一个函数实现字符串左旋转操作的功能。例如，输入字符串 `"abcdefg"` 和数字 `2`，输出结果为 `"cdefgab"`。

> 三次翻转即可。
>
> 参考代码:
>
> ```cpp
> class Solution {
> public:
>     string LeftRotateString(string str, int n) {
>         if (n > str.length() || n < 0) return string("");
>         string res(str);
>         reverse(begin(res), begin(res)+n);
>         reverse(begin(res)+n, end(res));
>         reverse(begin(res), end(res));
>         return res;
>     }
> };
> ```
