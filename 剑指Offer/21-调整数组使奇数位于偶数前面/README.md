# 题目描述

输入一个整数数组，实现一个函数来调整该数组中数字的顺序，使得所有的奇数位于数组的前半部分，所有的偶数位于数组的后半部分，并保证奇数和奇数，偶数和偶数之间的相对位置不变。

## 解题思路

若不要求相对位置不变，可采用双指针。一个从前往后指向奇数，一个从后往前指向偶数，遇到不符合的数字进行交换。

## 参考代码

将原数组中的偶数删除，使用额外空间保存偶数，最后在将偶数加到原数组后面:

```cpp
class Solution {
public:
    void reOrderArray(vector<int> &array) {
        if (array.size() == 0) return;
        vector<int> veven;
        for (auto iv = array.begin(); iv != array.end();) {
            if ((*iv & 1) == 0) {
                veven.push_back(*iv);
                iv = array.erase(iv);
            } else {
                iv++;
            }
        }
        for (auto &x : veven) {
            array.push_back(x);
        }
    }
};
```

不使用额外空间保存数组，直接在原数组上进行交换:

```cpp
class Solution {
public:
    void reOrderArray(vector<int> &array) {
        int numOfOdd = count_if(array.begin(), array.end(), isOdd);
        reOrderArray(array.begin(), numOfOdd, array.size() - numOfOdd);
    }
    void reOrderArray(vector<int>::iterator start, int odd, int even) {
        if (odd == 0 || even == 0) return;
        int numOfOdd = 0, i;
        numOfOdd = count_if(start, start+odd, isOdd);
        reOrderArray(start, numOfOdd, odd-numOfOdd);        // 处理前半部分
        numOfOdd = count_if(start+odd, start+odd+even, isOdd);
        reOrderArray(start+odd, numOfOdd, even-numOfOdd);    // 处理后半部分
        for (i = 0; start[i] & 1; ++i);    // 找到前半部分的偶数开始位置
        if (i < odd) {                     // 将前半偶数和后半奇数部分进行交换
            reverse(start+i, start+odd+odd-i);
            reverse(start+i, start+odd);
            reverse(start+odd, start+odd+odd-i);
        }
    }
    static bool isOdd(int &x) { return x & 1; }
};
```
