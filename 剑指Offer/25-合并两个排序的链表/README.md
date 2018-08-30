# 题目描述

输入两个单调递增的链表，输出两个链表合成后的链表，当然我们需要合成后的链表满足单调不减规则。

## 解题思路

直接按递增顺序合并。

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
    ListNode* Merge(ListNode* pHead1, ListNode* pHead2)
    {
        if (pHead1 == nullptr) return pHead2;
        if (pHead2 == nullptr) return pHead1;
        ListNode *pHead, *pCurrent;
        if (pHead1->val >= pHead2->val) {
            pHead = pHead2;
            pHead2 = pHead2->next;
        } else {
            pHead = pHead1;
            pHead1 = pHead1->next;
        }
        pCurrent = pHead;
        while (pHead1 != nullptr && pHead2 != nullptr) {
            if (pHead1->val >= pHead2->val) {
                pCurrent->next = pHead2;
                pHead2 = pHead2->next;
            } else {
                pCurrent->next = pHead1;
                pHead1 = pHead1->next;
            }
            pCurrent = pCurrent->next;
        }
        if (pHead1 != nullptr)
            pCurrent->next = pHead1;
        if (pHead2 != nullptr)
            pCurrent->next = pHead2;
        return pHead;
    }
};
```