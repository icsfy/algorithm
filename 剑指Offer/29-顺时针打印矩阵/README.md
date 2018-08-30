# 题目描述

输入一个矩阵，按照从外向里以顺时针的顺序依次打印出每一个数字。

## 示例

输入如下4 X 4矩阵：

```
 1  2  3  4
 5  6  7  8
 9 10 11 12
13 14 15 16
```

则依次打印出数字

```
1,2,3,4,8,12,16,15,14,13,9,5,6,7,11,10.
```

## 解题思路

从左到右，从上到下，从右到左，从下到上四种状态转换。

## 参考代码

```cpp
class Solution {
public:
    vector<int> printMatrix(vector<vector<int>> matrix) {
        vector<int> result;
        int rows = matrix.size();
        if (rows == 0) return result;
        int cols = matrix[0].size();
        int x = 0, y = 0, status = 1;
        int x_max = cols - 1, y_max = rows - 1, x_min = 0, y_min = 0;
        for (int i = 0; i < rows * cols; ++i) {
            switch (status) {
                case 1:
                    result.push_back(matrix[y][x++]);
                    if (x > x_max) {
                        x--; y++; status = 2; y_min++;
                    }
                    break;
                case 2:
                    result.push_back(matrix[y++][x]);
                    if (y > y_max) {
                        y--; x--; status = 3; x_max--;
                    }
                    break;
                case 3:
                    result.push_back(matrix[y][x--]);
                    if (x < x_min) {
                        x++; y--; status = 4; y_max--;
                    }
                    break;
                case 4:
                    result.push_back(matrix[y--][x]);
                    if (y < y_min) {
                        y++; x++; status = 1; x_min++;
                    }
                    break;
            }
        }
        return result;
    }
};
```
