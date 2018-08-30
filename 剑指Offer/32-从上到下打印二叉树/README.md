# 题目描述

从上往下打印出二叉树的每个节点，同层节点从左至右打印。

## 解题思路

用队列实现按层遍历。

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
    vector<int> PrintFromTopToBottom(TreeNode* root) {
        vector<int> result;
        deque<TreeNode*> dq;
        dq.push_back(root);
        while (dq.size())
        {
            TreeNode *pNode = dq.front();
            dq.pop_front();
            if (pNode)
            {
                result.push_back(pNode->val);
                if (pNode->left) dq.push_back(pNode->left);
                if (pNode->right) dq.push_back(pNode->right);
            }
        }
        return result;
    }
};
```

## 相关题目

1. 从上到下按层打印二叉树，同一层节点从左至右输出。每一层输出一行。

> 先取得队列中元素的个数(即当前层元素的个数)记为n，则当处理完n个元素(即处理完当前层n个元素，此时队列中元素为下一层的元素)之后，再重新取得队列中元素的个数(即下一层元素的个数)。
>
> 参考代码：
> ```cpp
> /*
> struct TreeNode {
>     int val;
>     struct TreeNode *left;
>     struct TreeNode *right;
>     TreeNode(int x) :
>             val(x), left(NULL), right(NULL) {
>     }
> };
> */
> class Solution {
> public:
>     vector<vector<int> > Print(TreeNode* pRoot) {
>         vector<vector<int>> vvi;
>         if (pRoot == nullptr) return vvi;
>         deque<TreeNode*> dq;
>         dq.push_back(pRoot);
>         while (!dq.empty())
>         {
>             vector<int> vi;
>             int num = dq.size();
>             while (num--)
>             {
>                 TreeNode *pNode = dq.front();
>                 dq.pop_front();
>                 vi.push_back(pNode->val);
>                 if (pNode->left) dq.push_back(pNode->left);
>                 if (pNode->right) dq.push_back(pNode->right);
>             }
>             vvi.push_back(vi);
>         }
>         return vvi;
>     }
> };
> ```

2. 请实现一个函数按照之字形打印二叉树，即第一行按照从左到右的顺序打印，第二层按照从右至左的顺序打印，第三行按照从左到右的顺序打印，其他行以此类推。

> 用两个栈，奇数层左子树先入栈，偶数层右子树先入栈。
>
> 参考代码：
> ```cpp
> /*
> struct TreeNode {
>     int val;
>     struct TreeNode *left;
>     struct TreeNode *right;
>     TreeNode(int x) :
>             val(x), left(NULL), right(NULL) {
>     }
> };
> */
> class Solution {
> public:
>     vector<vector<int> > Print(TreeNode* pRoot) {
>         vector<vector<int>> vvi;
>         if (pRoot == nullptr) return vvi;
>         stack<TreeNode*> s[2];
>         // flag == 0: s[1]左子节点先入栈
>         // flag == 1: s[0]右子节点先入栈
>         bool flag = 0;
>         s[flag].push(pRoot);
>         while (!s[flag].empty())
>         {
>             vector<int> vi;
>             while (!s[flag].empty())
>             {
>                 TreeNode *pNode = s[flag].top();
>                 s[flag].pop();
>                 vi.push_back(pNode->val);
>                 if (flag == 0) {
>                     if (pNode->left) s[!flag].push(pNode->left);
>                     if (pNode->right) s[!flag].push(pNode->right);
>                 } else {  /* flag == 1 */
>                     if (pNode->right) s[!flag].push(pNode->right);
>                     if (pNode->left) s[!flag].push(pNode->left);
>                 }
>             }
>             flag = !flag;
>             vvi.push_back(vi);
>         }
>         return vvi;
>     }
> };
> ```
