title: Leetcode解题-Single Number II
date: 2015-08-25 11:50:49
tags: [Leetcode, Array, 位运算]
categories: [编程题]
---

## 描述
> Given an array of integers, every element appears three times except for one. Find that single one.
>
> Note:
> Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?

## 分析

这次变成了其他数字出现3次，不是偶数次，所以直接使用异或是行不通的，我们可以用一个长度为32（int的位数）的数组来记录每一个位上出现的次数，如果不是3的倍数则提取出来，组成结果的数。这个算法是空间`O(1)`的，因为数组大小固定是32，有点基排序的意思，但显得不那么优雅。可以用三个变量来代替这32个变量，模拟三进制运算：用`ones`记录二进制1出现1次（mod 3余1）的位数，`twos`记录二进制1出现2次（mod 3余2）的位数，出现3次时该位清零。

## 代码

### 固定大小数组
```python
class Solution(object):
    def singleNumber(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        s = 32
        b = [0] * s
        for x in nums:
            for i in xrange(s):
                f = (1 << i) & x
                if f:
                    b[i] += 1

        ret = 0
        for i in xrange(s):
            if b[i] % 3 != 0:
                ret |= 1 << i
        return ret if b[-1] % 3 == 0 else ret - (1 << s)
```

### 模拟三进制
```python
class Solution(object):
    def singleNumber(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        ones, twos, xthrees = 0, 0, 0
        for x in nums:
            twos |= (ones & x)  # 这时候twos里包括了2次或3次的
            ones ^= x  # 这时候ones中包括了出现1次或者3次的
            xthrees = ~(ones & twos)  # xthrees里包括了出现1次或2次的
            ones &= xthrees
            twos &= xthrees
        return ones
```


