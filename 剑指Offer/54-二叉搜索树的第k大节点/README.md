# 题目描述

给定一棵二叉搜索树，请找出其中的第k小的结点。

## 示例

如下二叉搜索树中，按节点数值大小顺序，第三小结点的值为4。

```
        5
       / \
      3   7
     / \ / \
    2  4 6  8
```

## 解题思路

中序遍历。

## 参考代码

```cpp
/*
struct TreeNode {
    int val;
    struct TreeNode *left;
    struct TreeNode *right;
    TreeNode(int x) :
            val(x), left(NULL), right(NULL) {
    }
};
*/
class Solution {
public:
    TreeNode* KthNode(TreeNode* pRoot, int k)
    {
        if (pRoot == nullptr || k == 0) return nullptr;
        return KthNodeCore(pRoot, k);
    }
    TreeNode* KthNodeCore(TreeNode* pRoot, int &k)
    {
        TreeNode *target = nullptr;
        if (pRoot->left)
            target = KthNodeCore(pRoot->left, k);
        if (target == nullptr) {
            if (k == 1) target = pRoot;
            k--;
        }
        if (target == nullptr && pRoot->right)
            target = KthNodeCore(pRoot->right, k);
        return target;
    }
};
```
