# 题目描述

输入两个树节点，求它们的最低公共祖先。

## 示例

输入节点 F 和 H，输出 B。

```
          A
         / \
        B   C
      /   \
     D      E
    / \   / | \
   F  G   H I  J
```

## 解题思路

用两个链表分别保存从根节点到输入的两个节点的路径，然后把问题转换成两个链表的最后公共节点。

## 参考代码

```cpp
class Solution {
public:
    TreeNode* GetLastCommonParent(TreeNode* root, TreeNode* pNode1, TreeNode* pNode2) {
        if (root == nullptr || pNode1 == nullptr || pNode2 == nullptr)
            return nullptr;

        list<TreeNode*> path1, path2;
        GetNodePath(root, pNode1, path1);
        GetNodePath(root, pNode2, path2);
        return GetLastCommonNode(path1, path2);
    }
    bool GetNodePath(TreeNode* root, TreeNode* pNode, list<TreeNode*>& path) {
        if (root == pNode) return true;
        path.push_back(root);
        bool found = false;
        for (auto &x : root->child) {
            if (found) break;
            found = GetNodePath(x, pNode, path);
        }
        if (!found) path.pop_back();
        return found;
    }
    TreeNode* GetLastCommonNode(list<TreeNode*>& p1, list<TreeNode*>& p2) {
        TreeNode* pNode = nullptr;
        auto iter1 = p1.begin(), iter2 = p2.begin();
        for (; iter1 != p1.end() && iter2 != p2.end(); ++iter1, ++iter2)
            if (*iter1 == *iter2) pNode = *iter1;
        return pNode;
    }
}
```
