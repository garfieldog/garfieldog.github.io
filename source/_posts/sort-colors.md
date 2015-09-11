title: Leetcode解题-Sort Colors
date: 2015-09-11 11:30:10
tags: [Leetcode, Array, Sorting]
categories: [编程题]
---

## 描述
> Given an array with n objects colored red, white or blue, sort them so that objects of the same color are adjacent, with the colors in the order red, white and blue.
>
> Here, we will use the integers 0, 1, and 2 to represent the color red, white, and blue respectively.
>
> Note:
> You are not suppose to use the library's sort function for this problem.
> Follow up:
> A rather straight forward solution is a two-pass algorithm using counting sort.
> First, iterate the array counting number of 0's, 1's, and 2's, then overwrite array with total number of 0's, then 1's and followed by 2's.
>
> Could you come up with an one-pass algorithm using only constant space?

## 分析
使用计数排序很简单。题目进阶要求只扫一遍数组，就有点意思了。可以用两指针左右夹逼，遇到0就放到前面，遇到2就放到后面，比较像快排中的partition。

## 代码
### 计数排序
```python
class Solution(object):
    def sortColors(self, nums):
        """
        :type nums: List[int]
        :rtype: void Do not return anything, modify nums in-place instead.
        """
        counts = [0, 0, 0]
        for x in nums:
            counts[x] += 1
        i = 0
        for j in xrange(len(counts)):
            for k in xrange(counts[j]):
                nums[i] = j
                i += 1
```

### 两指针
```python
class Solution(object):
    def sortColors(self, nums):
        """
        :type nums: List[int]
        :rtype: void Do not return anything, modify nums in-place instead.
        """
        pivot = 1
        i = 0
        j = len(nums) - 1
        k = i
        while k <= j:
            if nums[k] < pivot:
                if k == i:
                    k += 1
                    i += 1
                else:
                    nums[k], nums[i] = nums[i], nums[k]
                    i += 1
            elif nums[k] > pivot:
                nums[k], nums[j] = nums[j], nums[k]
                j -= 1
            else:
                k += 1
```
