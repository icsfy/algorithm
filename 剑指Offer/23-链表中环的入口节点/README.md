# 题目描述

给一个链表，若其中包含环，请找出该链表的环的入口节点，否则，输出null。

## 解题思路

快慢指针。一个指针每次走一步，另一个指针每次走两步。

- 若有环，则快指针会追上慢指针。
  - 接下来一个指针不变，另一个指针指向头节点，两个指针每次走一步，最终会在环的入口节点相遇。
- 若没有环，则快指针走到链表末尾时都不会跟慢指针相遇。

## 参考代码

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
    ListNode* EntryNodeOfLoop(ListNode* pHead)
    {
        if (pHead == nullptr) return nullptr;
        ListNode *p1, *p2;
        p1 = p2 = pHead;
        do {
            p1 = p1->next;
            p2 = p2->next;
            if (p2) p2 = p2->next;
        } while (p1 != p2 && p1 != nullptr && p2 != nullptr);
        if (p1 == p2 && p2 != nullptr) {
            p1 = pHead;
            while (p1 != p2) {
                p1 = p1->next;
                p2 = p2->next;
            }
        }
        return p2;
    }
};
```
