# 题目描述

输入一棵二叉树，求该树的深度。从根结点到叶结点依次经过的结点（含根、叶结点）形成树的一条路径，最长路径的长度为树的深度。

## 解题思路

递归遍历左右子树得到树的深度。或者按层遍历得到树的深度。

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
    int TreeDepth(TreeNode* pRoot)
    {
        // 递归法
        //return pRoot ? max(TreeDepth(pRoot->left), TreeDepth(pRoot->right)) + 1 : 0;
        int depth = 0;
        if (pRoot)
        {
            queue<TreeNode*> q;
            q.push(pRoot);
            while (q.size())
            {
                depth++;
                int size = q.size();
                for (int i = 0; i < size; ++i) {
                    TreeNode *p = q.front();
                    q.pop();
                    if (p->left) q.push(p->left);
                    if (p->right) q.push(p->right);
                }
            }
        }
        return depth;
    }
};
```

## 相关题目

1. 输入一棵二叉树的根节点，判断该树是不是平衡二叉树。如果某二叉树中任意节点的左右子树的深度相差不超过1，那么它就是一棵平衡二叉树。

> 后序遍历，在遍历每个节点时记录深度
>
> 参考代码：
> ```cpp
> class Solution {
> public:
>     bool IsBalanced_Solution(TreeNode* pRoot) {
>         int depth = 0;
>         return IsBalanced(pRoot, &depth);
>     }
>     bool IsBalanced(TreeNode* pRoot, int *depth) {
>         if (pRoot == nullptr) {
>             *depth = 0;
>             return true;
>         }
>         int left, right;
>         if (IsBalanced(pRoot->left, &left) && IsBalanced(pRoot->right, &right)) {
>             int diff = left - right;
>             if (diff <= 1 && diff >= -1) {
>                 *depth = (left > right ? left : right) + 1;
>                 return true;
>             }
>         }
>         return false;
>     }
> };
> ```