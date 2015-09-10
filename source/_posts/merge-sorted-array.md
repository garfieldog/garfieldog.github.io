title: Leetcode解题-Merge Sorted Array
date: 2015-09-10 10:33:49
tags: [Leetcode, Array, Sorting]
categories: [编程题]
---

## 描述
> Given two sorted integer arrays nums1 and nums2, merge nums2 into nums1 as one sorted array.
>
> Note:
> You may assume that nums1 has enough space (size that is greater or equal to m + n) to hold additional elements from nums2. The number of elements initialized in nums1 and nums2 are m and n respectively.

## 分析
要`in-place`，就不能从前向后扫，要从后往前扫，不难，但要争取一遍写出无错的。时间复杂度`O(m + n)`，空间`O(1)`。

## 代码
### Python
```python
class Solution(object):
    def merge(self, nums1, m, nums2, n):
        """
        :type nums1: List[int]
        :type m: int
        :type nums2: List[int]
        :type n: int
        :rtype: void Do not return anything, modify nums1 in-place instead.
        """
        i = m - 1
        j = n - 1
        while i >= 0 and j >= 0:
            if nums1[i] > nums2[j]:
                nums1[i + j + 1] = nums1[i]
                i -= 1
            else:
                nums1[i + j + 1] = nums2[j]
                j -= 1
        while j >= 0:
            nums1[j] = nums2[j]
            j -= 1
```
