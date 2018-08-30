# 题目描述

请实现两个函数，分别用来序列化和反序列化二叉树

## 解题思路

前序遍历。`nullptr` 指针序列化为特殊字符，节点的数值之间需要隔开。

## 参考代码

```cpp
/*
struct TreeNode {
    int val;
    struct TreeNode *left;
    struct TreeNode *right;
    TreeNode(int x) :
            val(x), left(NULL), right(NULL) {
    }
};
*/
class Solution {
public:
    char* Serialize(TreeNode *root) {
        if (!root) return nullptr;
        string s;
        deque<TreeNode*> q;
        q.push_back(root);
        while (q.size()) {
            int n = q.size();
            while (n--) {
                if (q.front()) {
                    q.push_back(q.front()->left);
                    q.push_back(q.front()->right);
                    s += to_string(q.front()->val) + ' ';
                } else {
                    s += "# ";
                }
                q.pop_front();
            }
        }
        char *p = strdup(s.c_str());
        return p;
    }
    TreeNode* Deserialize(char *str) {
        if (str == nullptr) return nullptr;
        auto ret = nextNode(&str);
        deque<TreeNode*> q;
        q.push_back(ret);
        while (q.size()) {
            int n = q.size();
            while (n--) {
                q.front()->left = nextNode(&str);
                q.front()->right = nextNode(&str);
                if (q.front()->left)
                    q.push_back(q.front()->left);
                if (q.front()->right)
                    q.push_back(q.front()->right);
                q.pop_front();
            }
        }
        return ret;
    }
    TreeNode* nextNode(char **str) {
        string s;
        while (**str != '\0' && **str != ' ') {
            if (**str == '#') {
                *str += 2;
                return nullptr;
            }
            s += **str;
            ++*str;
        }
        if (**str == ' ') ++*str;
        return s.empty() ? nullptr : new TreeNode(stoi(s));
    }
};
```
