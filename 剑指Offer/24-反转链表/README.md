# 题目描述

输入一个链表，反转链表后，输出新链表的表头。

## 解题思路

注意需要保存当前节点、前一个节点和后一个节点。

## 参考代码

```cpp
/*
struct ListNode {
    int val;
    struct ListNode *next;
    ListNode(int x) :
            val(x), next(NULL) {
    }
};*/
class Solution {
public:
    ListNode* ReverseList(ListNode* pHead) {
        if (pHead == nullptr) return nullptr;
        ListNode *pCurrent, *pPrevious, *pNext;
        pCurrent = pHead->next;
        pPrevious = pHead;
        pHead->next = nullptr;
        while (pCurrent != nullptr) {
            pNext = pCurrent->next;
            pCurrent->next = pPrevious;
            pPrevious = pCurrent;
            pCurrent = pNext;
        }
        return pPrevious;
    }
};
```
