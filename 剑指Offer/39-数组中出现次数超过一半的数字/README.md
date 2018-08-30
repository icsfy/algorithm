# 题目描述

数组中有一个数字出现的次数超过数组长度的一半，请找出这个数字。例如输入一个长度为9的数组{1,2,3,2,2,2,5,4,2}。由于数字2在数组中出现了5次，超过数组长度的一半，因此输出2。如果不存在则输出0。

## 解题思路

不同的数字相互抵消。

## 参考代码

```cpp
class Solution {
public:
    int MoreThanHalfNum_Solution(vector<int> numbers) {
        int length = numbers.size();
        if (length == 0) return 0;
        int result = numbers[0];
        int times = 1;
        for (int i = 1; i < length; ++i) {
            if (times == 0) {
                result = numbers[i];
                times = 1;
            } else if (numbers[i] == result) {
                times++;
            } else {
                times--;
            }
        }
        result = count(numbers.begin(), numbers.end(), result) > numbers.size()/2
                    ? result : 0;
        return result;
    }
};
```
