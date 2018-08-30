# 题目描述

从扑克牌中随机抽出5张牌，判断是不是一个顺子，即这5张牌是不是连续的。
2~10 为数字本身，A 为 1，J 为 11，Q 为 12，K 为 13，而大小王可以看成任意数字（为了方便起见,把大小王都定义为 0）。

## 示例

输入：数组 `{0,1,3,4,5}`

输出：`true`

## 解题思路

统计数组中 0 的个数和其它数字，用 0 填补空位。

## 参考代码

```cpp
class Solution {
public:
    bool IsContinuous( vector<int> numbers ) {
        int zeros = 0, others = 0;
        for (auto &x : numbers) {
            if (x == 0) zeros++;    /* 统计0的个数 */
            else if ((others & (1 << x)) == 0) others |= 1 << x;  /* 将对应位置1 */
            else return false;    /* 有重复数字，对子 */
        }
        if (others != 0) {
            while ((others & 1) == 0) others >>= 1;  /* 最右位1移到最右 */
            while (others != 0) {
                if ((others & 1) == 0)    /* 遇到空位 */
                    if (zeros-- == 0)    /* 判断有没有大小王 */
                        break;
                others >>= 1;    /* 处理下一位 */
            }
            if (others == 0) return true;    /* 处理完毕，不是因为没有大小王才break出来 */
        }
        return false;
    }
};
```
