# 题目描述

把 n 个骰子扔在地上，所有骰子朝上一面的点数之和为 s。输入 n，打印出 s 的所有可能的值出现的概率。

## 解题思路

感觉这个不是最优解。。

## 参考代码

```cpp
class Solution {
public:
    void PrintProbability(int n) {
        if (n < 1) return;
        int *p[2];
        p[0] = new int[6 * n + 1];
        p[1] = new int[6 * n + 1];
        for (int i = 0; i < 6 * n + 1; ++i)
            p[0][i] = p[1][i] = 0;
        bool flag = 0;
        for (int i = 1; i <= 6; ++i)
            p[flag][i] = 1;

        for (int k = 2; k <= n; ++k) {
            for (int i = 0; i < k; ++i)
                p[!flag][i] = 0;
            for (int i = k; i <= 6 * k; ++i) {
                p[!flag][i] = 0;
                for (int j = 1; j <= i && j <= 6; ++j)
                    p[!flag][i] += p[flag][i-j];
            }
            flag = !flag;
        }

        double total = pow(6, n);
        for (int i = n; i <= 6 * n; ++i) {
            double ratio = p[flag][i] / total;
            printf("%d: %e\n", i, ratio);
        }

        delete [] p[0];
        delete [] p[1];
    }
}
```
