# 题目描述

输入一个链表，输出该链表中倒数第k个结点。

## 解题思路

双指针法，第一个指针先走k步，然后两个指针一起走，当第一个指针到达末尾时，第一个指针刚好指向倒数第k个节点。

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
    ListNode* FindKthToTail(ListNode* pListHead, unsigned int k) {
        ListNode *p1, *p2;
        p1 = p2 = pListHead;
        int i;
        for (i = 0; i < k && p2 != nullptr; ++i)
            p2 = p2->next;
        if (i != k) return nullptr;
        while (p2 != nullptr) {
            p1 = p1->next;
            p2 = p2->next;
        }
        return p1;
    }
};
```
