# 题目描述

输入一棵二叉搜索树，将该二叉搜索树转换成一个排序的双向链表。要求不能创建任何新的结点，只能调整树中结点指针的指向。

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
};*/
class Solution {
public:
    TreeNode* Convert(TreeNode* pRootOfTree)
    {
        TreeNode *pLastNodeInList = nullptr;
        ConvertNode(pRootOfTree, &pLastNodeInList);

        TreeNode *pHeadOfList = pLastNodeInList;
        while (pHeadOfList != nullptr && pHeadOfList->left != nullptr)
            pHeadOfList = pHeadOfList->left;
        return pHeadOfList;
    }
    void ConvertNode(TreeNode* pNode, TreeNode** pLastNodeInList) {
        if (pNode == nullptr) return;

        if (pNode->left != nullptr)
            ConvertNode(pNode->left, pLastNodeInList);

        pNode->left = *pLastNodeInList;
        if (*pLastNodeInList != nullptr)
            (*pLastNodeInList)->right = pNode;
        *pLastNodeInList = pNode;

        if (pNode->right != nullptr)
            ConvertNode(pNode->right, pLastNodeInList);
    }
};
```
