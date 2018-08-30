# 题目描述

在一个长度为n的数组里的所有数字都在 0 ~ n-1 的范围内。 数组中某些数字是重复的，但不知道有几个数字是重复的。也不知道每个数字重复几次。请找出数组中任意一个重复的数字。

## 示例

输入长度为 7 的数组 {2,3,1,0,2,5,3}，那么对应的输出是重复的数字 2 或者 3。

## 解题思路

重排数组。从头到尾依次扫描数组中的每个数字。

当扫描到下标为 i 的数字（记为 m）时：

- m 与 i 相等(数字和下标相等)，扫描下一个数字
- m 与 i 不等(数字和下标不等)，将 m 和下标为 m 的数字进行比较
  - m 与 下标为 m 的数字相等，则找到重复数字
  - m 与 下标为 m 的数字不等，则将这两个数字交换(将 m 放到属于它的位置)，接下来重复这个比较、交换的过程，直到发现重复数字。

## 参考代码

```cpp
class Solution {
public:
    // Parameters:
    //        numbers:     an array of integers
    //        length:      the length of array numbers
    //        duplication: (Output) the duplicated number in the array number
    // Return value:       true if the input is valid, and there are some duplications in the array number
    //                     otherwise false
    bool duplicate(int numbers[], int length, int* duplication) {
        if (numbers == nullptr || length < 2) return false;
        for (int i = 0; i < length; ++i) {
            while(numbers[i] != i) {
                if (numbers[numbers[i]] == numbers[i]) {
                    *duplication = numbers[i];
                    return true;
                }
                swap(numbers[i], numbers[numbers[i]]);
            }
        }
        return false;
    }
};
```
