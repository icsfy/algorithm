# 题目描述

请实现一个函数，用来判断一颗二叉树是不是对称的。注意，如果一颗二叉树和它的镜像是一样，那么它是对称的。

## 解题思路

定义一个针对前序遍历对称的遍历算法，先遍历父节点，再遍历它的右子节点，最后遍历它的左子结点。
遍历时考虑空指针。若前序遍历序列和对称前序遍历序列相同则是对称的。

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
    bool isSymmetrical(TreeNode* pRoot)
    {
        return isSymmetrical(pRoot, pRoot);
    }
    bool isSymmetrical(TreeNode *pRoot1, TreeNode *pRoot2)
    {
        if (pRoot1 == nullptr && pRoot2 == nullptr) return true;
        if (pRoot1 == nullptr || pRoot2 == nullptr) return false;
        if (pRoot1->val != pRoot2->val) return false;
        return isSymmetrical(pRoot1->left, pRoot2->right)
                && isSymmetrical(pRoot1->right, pRoot2->left);
    }
};
```
