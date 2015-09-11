title: Leetcode解题-First Missing Positive
date: 2015-09-11 10:44:36
tags: [Leetcode, Array, Sorting]
categories: [编程题]
---

## 描述
> Given an unsorted integer array, find the first missing positive integer.
>
> For example,
> Given [1,2,0] return 3,
> and [3,4,-1,1] return 2.
>
> Your algorithm should run in O(n) time and uses constant space.

## 分析
使用基排序的技巧，将对应数字交换到它对应的下标上去。注意如果被交换来的数字依然不是他应该在的位置，应该持续交换。最多需要交换`n`次。

要注意负数，越界数（大于数组长度的数）以及重复出现的数。

## 代码
### Python
```python
class Solution(object):
    def firstMissingPositive(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        n = len(nums)
        for i in xrange(n):
            while nums[i] > 0 and nums[i] <= n and nums[i] != i + 1:
                if nums[i] == nums[nums[i] - 1]:
                    break
                a = nums[i]
                nums[i] = nums[a - 1]
                nums[a - 1] = a

        i = 0
        while i < len(nums) and nums[i] == i + 1:
            i += 1
        return i + 1
```
