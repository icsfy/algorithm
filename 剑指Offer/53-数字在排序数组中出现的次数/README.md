# 题目描述

统计一个数字在排序数组中出现的次数。

## 示例

输入：排序数组 `{1,2,3,3,3,3,4,5}` 和数字 `3`

输出：`4`

## 解题思路

二分查找，找到第一个k和最后一个k，下标相减，时间复杂度O(logn)。

## 参考代码

```cpp
class Solution {
public:
    int GetNumberOfK(vector<int> data ,int k) {
        int cnt = 0;
        if (data.size() > 0) {
            int first = getFirstK(data, k, 0, data.size() - 1);
            int last = getLastK(data, k, 0, data.size() - 1);
            if (first > -1 && last > -1)
                cnt = last - first + 1;
        }
        return cnt;
    }
    /* 递归写法 */
    int getFirstK(vector<int> &data, int k, int start, int end) {
        if (start > end) return -1;
        int mid = (start + end) / 2;
        if (data[mid] == k) {
            if (mid > 0 && data[mid - 1] != k || mid == 0) return mid;
            else end = mid - 1;
        } else if (data[mid] > k)
            end = mid - 1;
        else  /* data[mid] < k */
            start = mid + 1;
        return getFirstK(data, k, start, end);
    }
    /* 循环写法 */
    int getLastK(vector<int> &data, int k, int start, int end) {
        while (start <= end) {
            int mid = (start + end) / 2;
            if (data[mid] < k)
                start = mid + 1;
            else if (data[mid] > k)
                end = mid - 1;
            else {  /* data[mid] == k */
                if (mid < end && data[mid + 1] != k || mid == end)
                    return mid;
                else start = mid + 1;
            }
        }
        return -1;
    }
};
```
