# 题目描述

输入一个整形数组，数组里有正数也有负数。数组中的一个或连续多个整数组成一个子数组。求所有子数组的和的最大值。要求时间复杂度为O(n)。

## 示例

输入数组 `{1,-2,3,10,-4,7,2,-5}`

和最大的子数组为 `{3,10,-4,7,2}`，因此输出为该子数组的和 `18`。

## 解题思路

从头到尾累加数组中的每个数字。和初始化为0，当和为负数时重新开始累加，记录最大和。

## 参考代码

```cpp
class Solution {
public:
    int FindGreatestSumOfSubArray(vector<int> array) {
        int curSum(0), greatestSum(0x80000000);
        for (int i = 0; i < array.size(); ++i) {
            if (curSum <= 0)
                curSum = array[i];
            else
                curSum += array[i];

            if (curSum > greatestSum)
                greatestSum = curSum;
        }
        return greatestSum;
    }
};
```
