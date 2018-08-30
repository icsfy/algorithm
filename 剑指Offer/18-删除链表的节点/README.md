# 题目描述

在一个排序的链表中，存在重复的结点，请删除该链表中重复的结点，重复的结点不保留，返回链表头指针。 例如，链表1->2->3->3->4->4->5 处理后为 1->2->5

## 解题思路

注意头节点重复的情况。

## 参考代码

递归法：

```cpp
/*
struct ListNode {
    int val;
    struct ListNode *next;
    ListNode(int x) :
        val(x), next(NULL) {
    }
};
*/
class Solution {
public:
    ListNode* deleteDuplication(ListNode* pHead)
    {
        if (pHead == nullptr || pHead->next == nullptr) return pHead;
        ListNode *pCur;
        if (pHead->val == pHead->next->val) {
            pCur = pHead->next->next;
            while (pCur != nullptr && pCur->val == pHead->val)
                pCur = pCur->next;
            return deleteDuplication(pCur);
        }
        pCur = pHead->next;
        pHead->next = deleteDuplication(pCur);
        return pHead;
    }
};
```

新建一个节点，防止头节点被删除的情况：

```cpp
/*
struct ListNode {
    int val;
    struct ListNode *next;
    ListNode(int x) :
        val(x), next(NULL) {
    }
};
*/
class Solution {
public:
    ListNode* deleteDuplication(ListNode* pHead)
    {
        if (pHead == nullptr || pHead->next == nullptr) return pHead;
        ListNode pNewHead(pHead->val - 1);
        pNewHead.next = pHead;
        ListNode *pCur = &pNewHead, *pNext = pHead;
        while (pNext) {
            while (pNext->next && pNext->next->val == pNext->val)
                pNext = pNext->next;
            if (pCur->next != pNext) {
                pNext = pNext->next;
                pCur->next = pNext;
            } else {
                pCur = pNext;
                pNext = pNext->next;
            }
        }
        return pNewHead.next;
    }
};
```
