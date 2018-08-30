# 题目描述

输入一个整数数组，判断该数组是不是某二叉搜索树的后序遍历的结果。如果是则输出Yes,否则输出No。假设输入的数组的任意两个数字都互不相同。

## 解题思路

递归遍历左右子树。

## 参考代码

```cpp
class Solution {
public:
    bool VerifySquenceOfBST(vector<int> sequence) {
        if (sequence.empty()) return false;
        return isBST(sequence.begin(), sequence.end() - 1);
    }
    bool isBST(const vector<int>::iterator &vstart, const vector<int>::iterator &vend) {
        int root = *vend;
        int i = 0;
        while (vstart[i] < root) ++i;
        int j = i;
        while (vstart[j] > root) ++j;
        if (vstart[j] != root) return false;
        bool left = true;
        if (i > 0) left = isBST(vstart, vstart + i - 1);
        bool right = true;
        if (i < vend - vstart - 1) right = isBST(vstart + i, vend - 1);
        return left && right;
    }
};
```
