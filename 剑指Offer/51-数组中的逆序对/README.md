# 题目描述

在数组中的两个数字，如果前面一个数字大于后面的数字，则这两个数字组成一个逆序对。输入一个数组,求出这个数组中的逆序对的总数P。并将P对1000000007取模的结果输出。 即输出P%1000000007

输入描述:

题目保证输入的数组中没有的相同的数字

数据范围：

    对于%50的数据,size<=10^4
    对于%75的数据,size<=10^5
    对于%100的数据,size<=2*10^5

## 示例

输入：
`1,2,3,4,5,6,7,0`

输出：
`7`

## 解题思路

先把数组分割成子数组，统计出子数组内部的逆序对的数目，然后再统计出两个相邻子数组
之间的逆序对的数目。在统计逆序对的过程中，还需要对数组进行排序（归并排序过程）。

## 参考代码

```cpp
class Solution {
public:
    int InversePairs(vector<int> data) {
        int length = data.size();
        if (length == 0) return 0;
        vector<int> copy(data);
        return InversePairsCore(data, copy, 0, length - 1);
    }
    long long InversePairsCore(vector<int> &data, vector<int> &copy,
                               int start, int end)
    {
        if (start == end) return 0;
        int length = (end - start) / 2;
        long long left = InversePairsCore(copy, data, start, start + length);
        long long right = InversePairsCore(copy, data, start + length + 1, end);
        int p1 = start + length, p2 = end, p3 = end;
        long long count = 0;
        while (p1 >= start && p2 > start + length) {
            if (data[p1] > data[p2]) {
                copy[p3--] = data[p1--];
                count += p2 - (start + length);
            } else
                copy[p3--] = data[p2--];
        }
        while (p1 >= start) copy[p3--] = data[p1--];
        while (p2 > start + length) copy[p3--] = data[p2--];
        return (left + right + count) % 1000000007;
    }
};
```
