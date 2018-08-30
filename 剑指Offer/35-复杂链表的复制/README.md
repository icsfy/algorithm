# 题目描述

输入一个复杂链表（每个节点中有节点值，以及两个指针，一个指向下一个节点，另一个特殊指针指向任意一个节点），返回结果为复制后复杂链表的head。（注意，输出结果中请不要返回参数中的节点引用，否则判题程序会直接返回空）

## 解题思路

分三步：

1. 复制每个节点链接在每个节点的后面
2. 设置复制出来节点的特殊指针指向原来指向的下一个节点
3. 拆分链表，奇数位置节点为原始链表，偶数位置节点为复制出来的链表

## 参考代码

```cpp
/*
struct RandomListNode {
    int label;
    struct RandomListNode *next, *random;
    RandomListNode(int x) :
            label(x), next(NULL), random(NULL) {
    }
};
*/
class Solution {
public:
    RandomListNode* Clone(RandomListNode* pHead)
    {
        CloneNodes(pHead);
        ConnectRandomNodes(pHead);
        return ReconnectNodes(pHead);
    }
    void CloneNodes(RandomListNode* pHead) {
        while (pHead != nullptr) {
            RandomListNode *pClone = new RandomListNode(pHead->label);
            pClone->next = pHead->next;
            pHead->next = pClone;
            pHead = pClone->next;
        }
    }
    void ConnectRandomNodes(RandomListNode* pHead) {
        while (pHead != nullptr) {
            if (pHead->random != nullptr) {
                pHead->next->random = pHead->random->next;
            }
            pHead = pHead->next->next;
        }
    }
    RandomListNode* ReconnectNodes(RandomListNode* pHead) {
        RandomListNode *pCloneHead = nullptr, *pCloneNode = nullptr;
        if (pHead != nullptr) {
            pCloneHead = pCloneNode = pHead->next;
            pHead->next = pCloneNode->next;
            pHead = pHead->next;
        }
        while (pHead != nullptr) {
            pCloneNode->next = pHead->next;
            pCloneNode = pCloneNode->next;
            pHead->next = pCloneNode->next;
            pHead = pHead->next;
        }
        return pCloneHead;
    }
};
```
