title: Leetcode解题-Remove Element
date: 2015-08-21 10:49:09
tags: [Leetcode, Array, 两指针]
categories: [编程题]
---

## 描述

> Given an array and a value, remove all instances of that value in place and return the new length.
>
> The order of elements can be changed. It doesn't matter what you leave beyond the new length.

删除数组中的给定元素。

## 分析

这是一道简单题，使用两指针，一个记录当前有效数组的尾部，一个遍历原数组。这样做的正确性在于，第一个指针之后、第二个指针之前的数组空间肯定是`安全的`（要么已经被复制到第一个指针之前的区域，要么是要删掉的值）。

## 代码

### Python
```python
class Solution(object):
    def removeElement(self, nums, val):
        """
        :type nums: List[int]
        :type val: int
        :rtype: int
        """
        i = 0
        for n in nums:
            if n != val:
                nums[i] = n
                i += 1
        return i
```
