# 338. Counting Bits

2018年8月16日

## 题目

Given a non negative integer number num. For every numbers i in the range 0 ≤ i ≤ num calculate the number of 1's in their binary representation and return them as an array.

Example 1:

```no
Input: 2
Output: [0,1,1]
```

Example 2:

```no
Input: 5
Output: [0,1,1,2,1,2]
```

Follow up:

- It is very easy to come up with a solution with run time O(n*sizeof(integer)). But can you do it in linear time O(n) /possibly in a single pass?
- Space complexity should be O(n).
- Can you do it like a boss? Do it without using any builtin function like __builtin_popcount in c++ or in any other language.

## 分析

给自己挖了一个新坑，选择了很低级的做法，日后再补。

根据十进制转化二进制的规则写一个函数，用来计算一个数转化为二进制后一的个数，然后在主函数内部循环调用这个函数，并不断将返回值添加到最重要返回的数组。

方法简单粗暴，本来以为会超时，但是并没有🤔

## 示例代码

C++

```cpp
class Solution {
public:
    int helper(int num){
        if(num ==1)
            return 1;
        if(num ==0)
            return 0;
        return helper(num / 2) + num % 2;
    }
    vector<int> countBits(int num) {
        vector<int> res;
        for(int i = 0; i <= num; i++){
            res.push_back(helper(i));
        }
        return res;
    }
};
```