title: Leetcode解题-去除有序数组中的重复元素 
date: 2015-08-18 16:34:22
tags: [Leetcode, Coding, Array]
categories: [编程题]
---

## 描述

> Given a sorted array, remove the duplicates in place such that each element appear only once and return the new length.
>
> Do not allocate extra space for another array, you must do this in place with constant memory.
>
> For example,
> Given input array nums = [1,1,2],
>
> Your function should return length = 2, with the first two elements of nums being 1 and 2 respectively. It doesn't matter what you leave beyond the new length.

给定一个排序后的数组，要求移除重复的元素，返回新的数组长度。要求O(1)空间

## 分析

这是一道简单题，使用两指针，一个记录去重后数组的尾部，一个扫原数组。可以实现inplace的时间O(n)空间O(1)的算法。另外，理解原题后就会发现，其实“有序”这个限定过于严格，只要保证相同的元素排列在一起就可以使用该算法。比如：[6, 6, 8, 8, 8, 7]

## 代码

#### Python
```python
class Solution:
    def removeDuplicates(self, nums):
        if not nums:
            return 0
        i = 1
        for n in nums[1:]:
            if n != nums[i]:
                nums[i] = n
                i += 1
        return i
```
