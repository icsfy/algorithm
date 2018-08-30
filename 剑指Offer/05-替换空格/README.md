# 题目描述

请实现一个函数，将一个字符串中的每个空格替换成 `"%20"`。

## 示例

输入:

```
"We Are Happy."
```

输出:

```
"We%20Are%20Happy."
```

## 解题思路

先遍历一次字符串，统计出字符串中空格总数，然后从字符串的后面开始往前复制和替换。时间复杂度 O(n).

## 参考代码

```cpp
class Solution {
public:
    void replaceSpace(char *str,int length) {
        if (str == NULL) return;
        int num_space = 0;
        char *p1, *p2;
        for (p1 = str; *p1 != '\0'; p1++) {
            if (*p1 == ' ')
                num_space++;
        }
        for (p2 = p1 + 2 * num_space; p1 >= str; --p1) {
            if (*p1 == ' ') {
                *p2-- = '0';
                *p2-- = '2';
                *p2-- = '%';
            } else {
                *p2-- = *p1;
            }
        }
    }
};
```
