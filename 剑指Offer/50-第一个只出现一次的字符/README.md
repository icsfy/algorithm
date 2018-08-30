# 题目描述

在一个字符串中找到第一个只出现一次的字符,并返回它的位置, 如果没有则返回 -1（需要区分大小写）.

## 解题思路

创建一个哈希表，第一次扫描统计各字符出现次数，第二次扫描返回第一个次数为1的值。

## 参考代码

```cpp
class Solution {
public:
    int FirstNotRepeatingChar(string str) {
        unordered_map<char, int> table;
        for (int i = 0; i < str.size(); ++i)
            table[str[i]]++;
        for (int i = 0; i < str.size(); ++i)
            if (table[str[i]] == 1)
                return i;
        return -1;
    }
};
```

## 相关问题

1. 请实现一个函数用来找出字符流中第一个只出现一次的字符。例如，当从字符流中只读出前两个字符"go"时，第一个只出现一次的字符是"g"。当从该字符流中读出前六个字符“google"时，第一个只出现一次的字符是"l"。（如果当前字符流没有存在出现一次的字符，返回#字符。）

> 用字符串的 ASCII 码作为哈希表的键值，把字符对应的位置作为哈希表的值。
> - 开始时数组中所有元素初始化为-1，
> - 当第一次从字符流中读出(值==-1)时更新对应值为字符流中的位置(保存了字符在字符流中的位置)，
> - 当再次读到相同字符(值>=0)时，值更新为-2。
>
> 参考代码：
> ```cpp
> class Solution
> {
> public:
>     Solution() : index(0) {
>         for (int i = 0; i < 256; ++i)
>             table[i] = -1;
>     }
>   //Insert one char from stringstream
>     void Insert(char ch)
>     {
>         if (table[ch] == -1)
>             table[ch] = index;
>         else if (table[ch] >= 0)
>             table[ch] = -2;
>         index++;
>     }
>   //return the first appearence once char in current stringstream
>     char FirstAppearingOnce()
>     {
>         char ch = '#';
>         int minIndex = numeric_limits<int>::max();
>         for (int i = 0; i < 256; ++i) {
>             if (table[i] >= 0 && table[i] < minIndex) {
>                 ch = (char)i;
>                 minIndex = table[i];
>             }
>         }
>         return ch;
>     }
> private:
>     // table[i]:
>     //    >=  0: has been found only once
>     //    == -1: has not found
>     //    == -2: has been found more than once
>     int table[256];
>     int index = 0;
> };
> ```
