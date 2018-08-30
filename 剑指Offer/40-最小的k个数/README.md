# 题目描述

输入n个整数，找出其中最小的K个数。例如输入4,5,1,6,2,7,3,8这8个数字，则最小的4个数字是1,2,3,4,。

## 解题思路

维护一个最大堆。

## 参考代码

```cpp
class Solution {
public:
    vector<int> GetLeastNumbers_Solution(vector<int> input, int k) {
        vector<int> v;
        if (k > 0 && k <= input.size()) {
            auto iter = input.begin();
            while (k--) {
                    v.push_back(*iter++);
                    push_heap(v.begin(), v.end());
            }
            while (iter != input.end()) {
                if (*iter < v[0]) {
                    pop_heap(v.begin(), v.end());
                    v.pop_back();
                    v.push_back(*iter);
                    push_heap(v.begin(), v.end());
                }
                ++iter;
            }
        }
        return v;
    }
};
```
