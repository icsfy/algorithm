# 题目描述

输入一颗二叉树的根节点和一个整数，打印出二叉树中节点值的和为输入整数的所有路径。路径定义为从树的根结点开始往下一直到叶结点所经过的结点形成一条路径。(注意: 在返回值的list中，数组长度大的数组靠前)

## 解题思路

用一个栈保存路径，访问节点时将该节点压栈，访问结束后将该节点弹出。

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
    vector<vector<int>> FindPath(TreeNode* root,int expectNumber) {
        vector<vector<int>> result;
        vector<int> path;
        FindPath(root, expectNumber, path, result);
        return result;
    }
    void FindPath(TreeNode *root, int expectNumber,
                  vector<int> &path, vector<vector<int>> &result) {
        if (root == nullptr) return;
        path.push_back(root->val);
        expectNumber -= root->val;
        bool isLeaf = root->left == nullptr && root->right == nullptr;
        if (0 == expectNumber && isLeaf) {
            result.push_back(path);
        } else {
            FindPath(root->left, expectNumber, path, result);
            FindPath(root->right, expectNumber, path, result);
        }
        path.pop_back();
    }
};
```
