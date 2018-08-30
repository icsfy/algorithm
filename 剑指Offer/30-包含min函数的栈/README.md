# 题目描述

定义栈的数据结构，请在该类型中实现一个能够得到栈中所含最小元素的min函数（时间复杂度应为O（1））。

## 解题思路

额外用一个辅助栈保存入栈时元素的最小值。

## 参考代码

```cpp
class Solution {
public:
    void push(int value) {
        s.push(value);
        if (min_s.empty())
            min_s.push(value);
        else if (value < min_s.top())
            min_s.push(value);
        else
            min_s.push(min_s.top());
    }
    void pop() {
        s.pop();
        min_s.pop();
    }
    int top() {
        return s.top();
    }
    int min() {
        return min_s.top();
    }
private:
    stack<int> s;
    stack<int> min_s;
};
```
