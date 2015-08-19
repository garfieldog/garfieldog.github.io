title: Leetcode解题-在被旋转的有序数组中查找目标II
date: 2015-08-19 10:25:25
tags: [Leetcode, Array, 二分法]
categories: [编程题]
---

## 描述

> Follow up for "Search in Rotated Sorted Array":
> What if duplicates are allowed?
>
> Would this affect the run-time complexity? How and why?
>
> Write a function to determine if a given target is in the array.

基本设定和[上一题][1]一样，但允许重复元素。
另外，本题只需要输出`True` or `False`即可，不需要输出下标。

## 分析

允许重复元素之后，`A[mid]`和`A[low]`就有可能相等，这种情况下我们就无法判断`A[mid]`是在哪个子数组中，这种情况下，我们可以简单地让`low`指针向前走一步。这样一来，算法最坏情况下时间复杂度增加到了O(n)，平均情况下仍然为O(log(n))。

## 代码

### Python
```python
class Solution:
    def search_r(self, A, target, low, high):
        mid = low + (high - low) / 2
        if A[mid] == target:
            return True
        if low >= high:
            return False
        if A[low] < A[mid]:
            # A[mid] locates in the first sub-array
            if A[low] <= target < A[mid]:
                return self.search_r(A, target, low, mid - 1)
            else:
                return self.search_r(A, target, mid + 1, high)
        elif A[low] == A[mid]:
            return self.search_r(A, target, low + 1, high)
        else:
            # A[mid] locates in the second sub-array
            if A[mid] < target <= A[high]:
                return self.search_r(A, target, mid + 1, high)
            else:
                return self.search_r(A, target, low, mid - 1)

    def search(self, nums, target):
        return self.search_r(nums, target, 0, len(nums) - 1)
```

[1]: /2015/08/18/search-in-rotated-sorted-array/
