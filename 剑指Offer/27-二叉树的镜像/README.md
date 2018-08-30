# 题目描述

操作给定的二叉树，将其变换为源二叉树的镜像。

输入描述:

二叉树的镜像定义：

```
源二叉树:
        8
       /  \
      6   10
     / \  / \
    5  7 9  11
镜像二叉树:
        8
       /  \
      10   6
     / \  / \
    11  9 7  5
```

## 解题思路

递归左右子树镜像。

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
};*/
class Solution {
public:
    void Mirror(TreeNode *pRoot) {
        if (pRoot == nullptr) return;
        TreeNode *pNode = pRoot->left;
        pRoot->left = pRoot->right;
        pRoot->right = pNode;
        Mirror(pRoot->left);
        Mirror(pRoot->right);
    }
};
```
