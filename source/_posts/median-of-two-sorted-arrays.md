title: Leetcode解题-找出两个有序数组的中位数
date: 2015-08-19 11:07:51
tags: [Leetcode, Array, 二分法]
categories: [编程题]
---

## 描述

> There are two sorted arrays nums1 and nums2 of size m and n respectively. Find the median of the two sorted arrays. The overall run time complexity should be O(log (m+n)).

给定两个有序的数组，长度分别问m和n，把这两个数组看成一个整体，求中位数。要求时间复杂度O(log(m+n))。中位数的定义是，如果一个集合有奇数`2k + 1`个元素，那排序后第k个数就是中位数，如果有偶数`2k`个元素，那么中位数的定义为排序后第`k`个数和第`k+1`个数的平均值。

## 分析

看时间复杂度的要求，首先想到的就是二分法，但是如何在两个数组上进行二分呢？我们把这个问题分解一下，先求解`在两个有序数组中查找整体第k大的数`，如果`m+n`是偶数，则调用两次子过程求平均，如果是奇数，调用一次。我们这样来找第k大的数：

1. 假设m和n都大于`k/2`，则比较`nums1[k/2 - 1]`和`nums2[k - k/2 - 1]`
2. 如果前者比较大，则可以扔掉`nums2[k - k/2 - 1]`之前的`k/2`个数
3. 如果后者比较大，则可以扔掉`nums1[k/2 - 1]`之前的`k/2`个数
4. 如果相等，说明第k个数已经找到

如果m和n中有一个小于`k/2`呢？假设n比m小，那么就取`min(k/2, n)`和`k - min(k/2, n)`作为比较的下标值。
时间复杂度是O(log(k))。在写代码的过程中，边界判断是非常容易出错的，要反复练习。

## 代码

### Python
```python
class Solution:
    # @param {integer[]} nums1
    # @param {integer[]} nums2
    # @return {float}
    def findMedianSortedArrays(self, nums1, nums2):
        total = len(nums1) + len(nums2)
        if total % 2 == 0:
            c1 = self.findKthInSortedArrays(nums1, nums2, total / 2)
            c2 = self.findKthInSortedArrays(nums1, nums2, total / 2 + 1)
            median = (c1 + c2) / 2.0
        else:
            median = float(self.findKthInSortedArrays(nums1, nums2, total / 2 + 1))
        return median

    def findKthInSortedArrays(self, nums1, nums2, k):
        return self.findKthInSortedArraysR(nums1, 0, len(nums1) - 1,
                                           nums2, 0, len(nums2) - 1, k)

    def findKthInSortedArraysR(self, nums1, x1, y1, nums2, x2, y2, k):
        m = y1 - x1 + 1
        n = y2 - x2 + 1
        if m < n:
            return self.findKthInSortedArraysR(nums2, x2, y2, nums1, x1, y1, k)
        if n == 0:
            return nums1[x1 + k - 1]

        if k == 1:
            return min(nums1[x1], nums2[x2])

        k2 = min(k / 2, n)
        k1 = k - k2
        if nums1[x1 + k1 - 1] == nums2[x2 + k2 - 1]:
            return nums1[x1 + k1 - 1]
        elif nums1[x1 + k1 - 1] > nums2[x2 + k2 - 1]:
            return self.findKthInSortedArraysR(nums1, x1, y1, nums2, x2 + k2, y2, k - k2)
        else:
            return self.findKthInSortedArraysR(nums1, x1 + k1, y1, nums2, x2, y2, k - k1)
```
