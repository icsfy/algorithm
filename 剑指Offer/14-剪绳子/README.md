# 题目描述

给你一根长度为 n 的绳子，请把绳子剪成 m 段（m、n 都是整数，n > 1 并且 m > 1），每段绳子长度记为 `k[0],k[1],...k[m]`。请问 `k[0]xk[1]x...xk[m]` 可能的最大乘积是多少？

## 示例

当绳子的长度为 8 时，把它剪成长度分别为 2、3、3 的三段，此时得到的最大乘积为 18。

## 解题思路

要使乘积最大：

- 当 `n >= 5` 时，尽可能多地剪成长度为 3 的绳子
- 当 `n == 4` 时，剪成两段长度为 2 的绳子

## 参考代码

```cpp
class Solution {
public:
    int maxProductAfterCutting(int length) {
        if (length < 2) return 0;
        if (length == 2) return 1;
        if (length == 3) return 2;

        int timesOf3 = length / 3;  // 尽可能多地剪去长度为 3 的绳子段

        if (length - timesOf3 * 3 == 1)
            timesOf3--;     // 剩下长度为 4 时应剪为长度为 2 的两段（2x2 > 3x1）

        int timesOf2 = (length - timesOf3 * 3) / 2;

        return pow(3, timesOf3) * pow(2, timesOf2);
    }
}
```
