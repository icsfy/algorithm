# 题目描述

请从字符串中找出一个最长的不包含重复字符的子字符串，计算该最长子字符串的长度。假设字符串中只包含 `'a'~'z'` 的字符。

## 示例

输入字符串 `"arabcacfr"`，最长不包含重复字符串的子字符串是 `"acfr"`，长度为 4。

## 解题思路

定义函数 f(i) 表示以第 i 个字符为结尾的不包含重复字符的子字符串的最长长度。从左到右逐一扫描字符串中的每一个字符。

- 如果第 i 个字符之前没有出现过，那么 `f(i) = f(i-1) + 1`
- 如果第 i 个字符之前已经出现过，计算第 i 个字符和它上次出现在字符串中的位置的距离，记为 d，分两种情况:
  - 若 `d <= f(i-1)`，则 `f(i) = d`
  - 若 `d > f(i-1)`，则 `f(i) = f(i-1) + 1`

## 参考代码

```cpp
class Solution {
public:
    int longestSubstringWithoutDuplication(const string& str) {
        int curlen = 0, maxlen = 0;
        int *pos = new int[26];
        for (int i = 0; i < 26; ++i) pos[i] = -1;
        for (int i = 0; i < str.length(); ++i) {
            int preIndex = pos[str[i] - 'a'];
            if (preIndex < 0 || i - preIndex > curlen)
                ++curlen;
            else {
                if (curlen > maxlen)
                    maxlen = curlen;
                curlen = i - preIndex;
            }
            pos[str[i] - 'a'] = i;
        }
        if (curlen > maxlen) maxlen = curlen;
        delete [] pos;
        return maxlen;
    }
}
```
