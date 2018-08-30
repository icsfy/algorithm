# 题目描述

输入一个正整数数组，把数组里所有数字拼接起来排成一个数，打印能拼接出的所有数字中最小的一个。

## 示例

输入数组{3，32，321}，则打印出这三个数字能排成的最小数字为321323。

## 解题思路

把数字转换成字符串，按照字符串大小的比较规则，对数组中的数字拼接进行排序。

## 参考代码

```cpp
class Solution {
public:
    string PrintMinNumber(vector<int> numbers) {
        sort(numbers.begin(), numbers.end(), [](const int& a, const int& b){
            return to_string(a) + to_string(b) < to_string(b) + to_string(a);
        });
        string result;
        for (auto &x : numbers)
            result += to_string(x);
        return result;
    }
};
```
