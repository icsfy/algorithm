# 题目描述

在一个 `m x n` 的棋盘的每一路都放有一个礼物，每个礼物都有一定的价值（价值大于 0）。你可以从棋盘的左上角开始拿格子里的礼物，并每次向右或者向下移动一格，直到到达棋盘的右下角。给定一个棋盘及其上面的礼物，请计算你最多能拿到多少价值的礼物？

## 示例

在下面的棋盘中，如果沿着路线: `1->12->5->7->7->16->5`，那么能拿到最大价值为 53 的礼物。

```
   1  10   3   8
  12   2   9   6
   5   7   4  11
   3   7  16   5
```

## 解题思路

动态规划。

定义一个函数 `f(x, y)` 表示到达坐标为 `(x, y)` 的格子时能拿到的礼物总和的最大值。根据题目要求，有两种到达坐标为 `(x, y)` 的路径：通过格子 `(x-1, y)` 或者 `(x, y - 1)`。所以 `f(x, y) = max(f(x-1, y), f(x, y-1)) + gift[x, y]`。
`gift[x, y]` 表示坐标为 `(x, y)` 的格子里礼物的价值。

## 参考代码

```cpp
class Solution {
public:
    int getMaxValue(const int* values, int rows, int cols) {
        if (values == nullptr || rows <= 0 || cols <= 0) return 0;
        int *maxVals = new int[cols];
        for (int i = 0; i < rows; ++i) {
            for (int j = 0; j < cols; ++j) {
                int left = 0, up = 0;
                if (i > 0) up = maxVals[j];
                if (j > 0) left = maxVals[j - 1];
                maxVals[j] = max(left, up) + values[i * cols + j];
            }
        }
        int maxVal = maxVals[cols - 1];
        delete [] maxVals;
        return maxVal;
    }
}
```
