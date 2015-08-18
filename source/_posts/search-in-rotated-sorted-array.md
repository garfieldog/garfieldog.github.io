title: Leetcode解题-在被旋转的有序数组中查找目标
date: 2015-08-18 23:33:09
tags: [Leetcode, Coding, Array, 二分法]
categories: [编程题]
---

## 描述

> Suppose a sorted array is rotated at some pivot unknown to you beforehand.
>
> (i.e., 0 1 2 4 5 6 7 might become 4 5 6 7 0 1 2).
>
> You are given a target value to search. If found in the array return its index, otherwise return -1.
>
> You may assume no duplicate exists in the array.

一个有序的数组可能在某个位置被旋转，比如[0, 1, 2, 4, 5, 6, 7]在4这个数字位置上被旋转后变为[4, 5, 6, 7, 0, 1, 2]，给定一个目标元素，查找这个元素在数组中的下标，如果不存在，返回-1。假设数组中没有重复值。

## 分析
在有序数组中查找目标，直接使用二分法即可。如果数组被旋转之后呢？考察这个数组的性质，它由两段有序子数组组成，并且，第一个子数组的任一个数都`大于`(因为数组没有重复值)第二个子数组的所有数。这样一来，我们仍然可以在这个数组上展开二分查找：当`A[mid] > A[low]`时，我们知道mid肯定落在第一个子数组里，反则反之。这时候我们再对比`target`和`A[low]`, `A[mid]`, `A[high]`的大小，从而判断接下来在那个半区搜索。

难点在边界条件的判断。

## 代码

### Python
```python
class Solution:
    def search_r(self, A, target, low, high):
        mid = low + (high - low) / 2
        if A[mid] == target:
            return mid
        if low >= high:
            return -1
        if A[low] <= A[mid]:
            # A[mid] locates in the first sub-array
            if A[low] <= target < A[mid]:
                return self.search_r(A, target, low, mid - 1)
            else:
                return self.search_r(A, target, mid + 1, high)
        else:
            # A[mid] locates in the second sub-array
            if A[mid] < target <= A[high]:
                return self.search_r(A, target, mid + 1, high)
            else:
                return self.search_r(A, target, low, mid - 1)

    def search(self, nums, target):
        return self.search_r(nums, target, 0, len(nums) - 1)
```
