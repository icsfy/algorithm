# 题目描述

给定一个二叉树和其中的一个结点，请找出中序遍历顺序的下一个结点并且返回。注意，树中的结点不仅包含左右子结点，同时包含指向父结点的指针。

## 解题思路

- 如果一个节点有右子树，那么它的下一个节点就是它的右子树中的最左子节点。
- 如果一个节点没有右子树：
  - 如果节点是它的父节点的左子节点，那么它的下一个节点就是它的父节点。
  - 如果节点是它的父节点的右子节点，沿着指向父节点的指针一直向上遍历，直到找到一个是它父节点的左子节点的节点。如果这样的节点存在，那么这个节点的父节点就是要找的下一个节点。

## 参考代码

```cpp
/*
struct TreeLinkNode {
    int val;
    struct TreeLinkNode *left;
    struct TreeLinkNode *right;
    struct TreeLinkNode *next;
    TreeLinkNode(int x) :val(x), left(NULL), right(NULL), next(NULL) {
    }
};
*/
class Solution {
public:
    TreeLinkNode* GetNext(TreeLinkNode* pNode)
    {
        if (pNode == nullptr) return nullptr;
        TreeLinkNode *pNext = nullptr;
        if (pNode->right) {    /* 有右子树 */
            pNext = pNode->right;
            while (pNext->left) pNext = pNext->left;  /* 找右子树中的最左子节点 */
        } else if (pNode->next) {    /* 有父节点 */
            pNext = pNode->next;
            while (pNext && pNode == pNext->right) {  // 若是父节点的右子树
                pNode = pNext;                        // 则向上遍历直到不是右子树
                pNext = pNext->next;                  // (即是父节点的左子树)
            }
        }
        return pNext;
    }
};
```
