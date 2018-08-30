# 题目描述

输入两个链表，找出它们的第一个公共结点。

## 解题思路

第一次遍历得到两个链表长度之差，第二次遍历找到相同节点。

## 参考代码

- 长度相同有公共结点，第一次就遍历到；没有公共结点，走到尾部NULL相遇，返回NULL。
- 长度不同有公共结点，第一遍差值就出来了，第二遍一起到公共结点；没有公共，一起到结尾NULL。

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
    ListNode* FindFirstCommonNode( ListNode* pHead1, ListNode* pHead2) {
        ListNode *p1 = pHead1, *p2 = pHead2;
        while (p1 != p2) {
            p1 = (p1 == nullptr ? pHead2 : p1->next);
            p2 = (p2 == nullptr ? pHead1 : p2->next);
        }
        return p1;
    }
};
```
