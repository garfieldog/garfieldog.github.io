title: Leetcode解题-Search for a Range
date: 2015-09-11 14:17:57
tags: [Leetcode, Array, 二分法]
categories: [编程题]
---

## 描述
> Given a sorted array of integers, find the starting and ending position of a given target value.
>
> Your algorithm's runtime complexity must be in the order of O(log n).
>
> If the target is not found in the array, return [-1, -1].
>
> For example,
> Given [5, 7, 7, 8, 8, 10] and target value 8,
> return [3, 4].

## 分析
可以先二分查找，再从中心向左右扩张。
但这样其实在某些极端情况下性能不佳，比如全是相同元素数组。可以用两次二分查找，一次找上界，一次找下界。

## 代码
### 先二分，后扩张
```python
class Solution(object):
    def searchRange(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """
        low = 0
        high = len(nums) - 1
        found = False
        while low <= high:
            mid = low + (high - low) / 2
            if nums[mid] == target:
                found = True
                break
            elif nums[mid] > target:
                high = mid - 1
            else:
                low = mid + 1
        if not found:
            return [-1, -1]

        i = mid - 1
        while i >= 0 and nums[i] == target:
            i -= 1
        j = mid + 1
        while j < len(nums) and nums[j] == target:
            j += 1
        return [i + 1, j - 1]
```

### 两次二分
```python
class Solution(object):
    def searchRange(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """
        lower = self.lowerBound(nums, target)
        upper = self.upperBound(nums, target)
        if lower >= len(nums) or nums[lower] != target:
            return [-1, -1]
        else:
            return [lower, upper]

    def upperBound(self, nums, target):
        low = 0
        high = len(nums) - 1
        while low <= high:
            mid = low + (high - low) / 2
            if nums[mid] <= target:
                low = mid + 1
            else:
                high = mid - 1
        return high

    def lowerBound(self, nums, target):
        low = 0
        high = len(nums) - 1
        while low <= high:
            mid = low + (high - low) / 2
            if nums[mid] >= target:
                high = mid - 1
            else:
                low = mid + 1
        return low
```
