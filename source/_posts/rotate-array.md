title: Leetcode解题-Rotate Array
date: 2015-08-26 11:56:18
tags: [Leetcode, Array]
categories: [编程题]
---

## 描述
> Rotate an array of n elements to the right by k steps.
>
> For example, with n = 7 and k = 3, the array [1,2,3,4,5,6,7] is rotated to [5,6,7,1,2,3,4].
>
> Note:
> Try to come up as many solutions as you can, there are at least 3 different ways to solve this problem.

## 分析
如果允许开新数组，那就太简单了，当然我们要找空间`O(1)`的解法。把原数组分为两段，分别翻转，然后把数组整体翻转，就得到了结果。

## 代码

### Python
```python
class Solution(object):
    def rotate(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: void Do not return anything, modify nums in-place instead.
        """
        k = (len(nums) - k) % len(nums)
        self.reverse(nums, 0, k - 1)
        self.reverse(nums, k, len(nums) - 1)
        self.reverse(nums, 0, len(nums) - 1)

    def reverse(self, nums, x, y):
        k = (y - x + 1) / 2
        for i in xrange(k):
            nums[x + i], nums[y - i] = nums[y - i], nums[x + i]
```
