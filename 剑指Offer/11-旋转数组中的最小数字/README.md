# 题目描述

把一个数组最开始的若干个元素搬到数组的末尾，我们称之为数组的旋转。 输入一个非减排序的数组的一个旋转，输出旋转数组的最小元素。 例如数组{3,4,5,1,2}为{1,2,3,4,5}的一个旋转，该数组的最小值为1。 NOTE：给出的所有元素都大于0，若数组大小为0，请返回0。

## 解题思路

二分查找，时间复杂度O(logn)

## 参考代码

```cpp
class Solution {
public:
    int minNumberInRotateArray(vector<int> rotateArray) {
        if (rotateArray.size() == 0) return 0;
        auto vstart = rotateArray.begin(), vend = rotateArray.end() - 1;
        auto vmid = vstart;
        while (*vstart >= *vend) {
            if (vend - vstart == 1) {
                vmid = vend;
                break;
            }
            vmid = vstart + (vend - vstart) / 2;
            if (*vstart == *vmid && *vmid == *vend)
                return minInOrder(rotateArray);
            if (*vmid >= *vstart)
                vstart = vmid;
            else
                vend = vmid;
        }
        return *vmid;
    }
    // 数组{1,0,1,1,1}和数组{1,1,1,0,1}可看成递增排序数组{0,1,1,1,1}的旋转
    // 由于开始、末尾、中间值相同，遍历处理，不能二分查找
    int minInOrder(vector<int> &v) {
        int minVal = v[0];
        for (auto &x : v)
            if (minVal > x)
                minVal = x;
        return minVal;
    }
};
```
