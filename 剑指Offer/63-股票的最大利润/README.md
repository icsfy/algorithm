# 题目描述

假设把某股票的价格按照事件先后顺序存储在数组中，请问买卖该股票一次可能获得的最大利润是多少？例如，一只股票在某些时间节点的价格为 `{9, 11, 16, 8, 5, 7, 12, 16, 14}`。如果我们能在价格为 5 的时候买入并在价格为 16 时卖出，则能收获最大的利润 11。

## 解题思路

存储最小值。时间复杂度O(n)

## 参考代码

```cpp
class Solution {
public:
    int MaxDiff(const int* numbers, unsigned length) {
        if (numbers == nullptr || length < 2) return 0;
        int min = numbers[0];
        int maxDiff = numbers[1] - min;
        for (int i = 2; i < length; ++i) {
            if (numbers[i - 1] < min)
                min = numbers[i-1];
            int currentDiff = numbers[i] - min;
            if (currentDiff > maxDiff)
                maxDiff = currentDiff;
        }
        return maxDiff;
    }
}
```
