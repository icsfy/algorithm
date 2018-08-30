# 题目描述

输入一个链表，按链表值从尾到头的顺序返回一个ArrayList。

## 解题思路

用栈或递归实现倒序打印。

## 参考代码

```cpp
/**
 *  struct ListNode {
 *        int val;
 *        struct ListNode *next;
 *        ListNode(int x) :
 *              val(x), next(NULL) {
 *        }
 *  };
 */
class Solution {
public:
    vector<int> printListFromTailToHead(ListNode* head) {
        vector<int> iv;
        printListReversingly(head, iv);
        return iv;
    }
    void printListReversingly(ListNode* head, vector<int> &iv) {
        if (head != NULL) {
            printListReversingly(head->next, iv);
            iv.push_back(head->val);
        }
    }
};
```
