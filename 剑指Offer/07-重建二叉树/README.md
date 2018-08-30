# 题目描述

输入某二叉树的前序遍历和中序遍历的结果，请重建出该二叉树。假设输入的前序遍历和中序遍历的结果中都不含重复的数字。例如输入前序遍历序列{1,2,4,7,3,5,6,8}和中序遍历序列{4,7,2,1,5,3,8,6}，则重建二叉树并返回。

## 解题思路

通过递归来构造左右子树。

## 参考代码

```cpp
/**
 * Definition for binary tree
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    TreeNode* reConstructBinaryTree(vector<int> pre,vector<int> vin) {
        return reConstructBinaryTreeCore(
            pre.begin(), pre.end(), vin.begin(), vin.end());
    }
    TreeNode* reConstructBinaryTreeCore(vector<int>::iterator startPre,
                                        vector<int>::iterator endPre,
                                        vector<int>::iterator startIn,
                                        vector<int>::iterator endIn)
    {
        if (startPre == endPre || startIn == endIn) return nullptr;
        TreeNode *root = new TreeNode(*startPre);
        for (auto i = startIn; i != endIn; ++i) {
            if (*startPre == *i) {
                root->left = reConstructBinaryTreeCore(
                    startPre + 1, startPre + (i - startIn) + 1, startIn, i);
                root->right = reConstructBinaryTreeCore(
                    startPre + (i - startIn) + 1, endPre, i + 1, endIn);
                break;
            }
        }
        return root;
    }
};
```
