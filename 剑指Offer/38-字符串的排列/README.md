# 题目描述

输入一个字符串,按字典序打印出该字符串中字符的所有排列。例如输入字符串abc,则打印出由字符a,b,c所能排列出来的所有字符串abc,acb,bac,bca,cab和cba。

## 解题思路

把字符串看成两部分：第一部分是它的第一个字符，第二部分是后面的字符。

- 第一步求所有可能出现在第一个位置的字符，即把第一个字符和后面所有的字符交换
- 第二部固定第一个字符，求后面所有字符的排列

## 参考代码

```cpp
class Solution {
public:
    vector<string> Permutation(string str) {
        vector<string> v;
        Permutation(str, 0, v);
        return v;
    }
    void Permutation(string str, int pos, vector<string> &result) {
        if (pos == str.length() && str.length() != 0) {
            result.push_back(str);
        } else {
            for (int i = pos; i != str.length(); ++i) {
                if (str[i] == str[pos] && i != pos) continue;
                {
                    swap(str[i], str[pos]);
                    Permutation(str, pos + 1, result);
                }
            }
        }
    }
};
```
