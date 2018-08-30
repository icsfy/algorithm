# 题目描述

`0,1,...,n-1` 这 n 个数字排成一个圆圈，从数字 0 开始，每次从这个圆圈里删除第 m 个数字。求出这个圆圈里剩下的最后一个数字。

## 示例

`0、1、2、3、4` 这 5 个数字组成一个圆圈，从数字 0 开始每次删除第 3 个数字，则删除的前 4 个数字依次是 `2、0、4、1`，因此最后剩下的数字是 3。

## 解题思路

环形链表模拟。

或者用公式：

```
f(n, m) = 0, n = 1
f(n, m) = [f(n-1, m) + m] % n, n > 1
```

## 参考代码

```cpp
class Solution {
public:
    int LastRemaining_Solution(int n, int m)
    {
        if (n < 1 || m < 1)
            return -1;

        int last = 0;
        for (int i = 2; i <= n; ++i)
            last = (last + m) % i;

        return last;
    }
};
```
