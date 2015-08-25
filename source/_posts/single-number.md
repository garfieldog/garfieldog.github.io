title: Leetcode解题-Single Number
date: 2015-08-25 11:32:03
tags: [Leetcode, Array, 数学]
categories: [编程题]
---

## 描述

> Given an array of integers, every element appears twice except for one. Find that single one.
>
> Note:
> Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?

## 分析
空间`O(n)`的算法很容易想，但是题目要求空间`O(1)`，这个就有一些奇技淫巧了，想到了就很容易，没想到还真是抓瞎。用`xor`操作的性质，给一个序列的数使用`xor`进行reduce，如果一个数出现偶数次，那么就跟没有出现过是一样的，也就是$ x \oplus y \oplus x = y $。

## 代码

### Python
```python
class Solution(object):
    def singleNumber(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        return reduce(lambda x, y: x ^ y, nums)
```

