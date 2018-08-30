# 题目描述

用两个栈来实现一个队列，完成队列的Push和Pop操作。 队列中的元素为int类型。

## 解题思路

`stack1` 用于入队，`stack2` 用于出队。

入队:

- 对 `stack1` 进行 `push`

出队:

- `stack2` 不为空，直接对 `stack2` 进行 `pop`
- `stack2` 为空，则将 `stack1` 所有元素 `pop` 存入 `stack2`, 再进行出队

## 参考代码

```cpp
class Solution
{
public:
    void push(int node) {
        stack1.push(node);
    }

    int pop() {
        if (stack2.empty()) {
            while(!stack1.empty()) {
                stack2.push(stack1.top());
                stack1.pop();
            }
        }
        int res = stack2.top();
        stack2.pop();
        return res;
    }

private:
    stack<int> stack1;
    stack<int> stack2;
};
```
