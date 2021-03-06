# 题目描述

在一个二维数组中（每个一维数组的长度相同），每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。

## 示例

```
1   2   8   9
2   4   9   12
4   7   10  13
6   8   11  15
```

查找数字 `7` 则返回 `true`，查找数字 `5` 则返回 `false`。

## 解题思路

从右上角或者左下角元素开始查找。

## 参考代码

```cpp
class Solution {
public:
    bool Find(int target, vector<vector<int>> array) {
        int i = 0, j = array[0].size() - 1;
        while (i < array.size() && j>= 0) {
            if (array[i][j] == target) return true;
            if (array[i][j] > target) --j;
            else ++i;
        }
        return false;
    }
};
```
