# 题目描述

输入一个正数 s，输出所有和为 s 的连续正数序列（至少含有两个数）。
例如：`15=1+2+3+4+5=4+5+6=7+8`

## 解题思路

双指针，当总和小于sum，大指针继续+，否则小指针+

## 参考代码

```cpp
class Solution {
public:
    vector<vector<int>> FindContinuousSequence(int sum) {
        vector<vector<int>> vvi;
        if (sum >= 3) {
            int small = 1, big = 2;
            int curSum = small + big;
            while (small < big) {
                if (curSum > sum)
                    curSum -= small++;
                else if (curSum < sum)
                    curSum += ++big;
                else {  /* curSum == sum */
                    vector<int> vi(big - small + 1);
                    std::iota(vi.begin(), vi.end(), small);
                    vvi.push_back(vi);
                    curSum -= small++;
                }
            }
        }
        return vvi;
    }
};
```
