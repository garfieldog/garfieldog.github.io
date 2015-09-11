title: Leetcode解题-Search Insert Position
date: 2015-09-11 15:11:39
tags: [Leetcode, Array, 二分法]
categories: [编程题]
---

## 描述
> Given a sorted array and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.
>
> You may assume no duplicates in the array.
>
> Here are few examples.
> [1,3,5,6], 5 → 2
> [1,3,5,6], 2 → 1
> [1,3,5,6], 7 → 4
> [1,3,5,6], 0 → 0

## 分析
其实就是上一题[Search for a Range][1]实现的`lowerBound`。

## 代码
### Python
```python
class Solution(object):
    def searchInsert(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: int
        """
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

[1]: /2015/09/11/search-for-a-range/
