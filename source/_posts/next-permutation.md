title: Leetcode解题-Next Permutation
date: 2015-08-21 11:07:02
tags: [Leetcode, Array, Permutation]
categories: [编程题]
---

## 描述

> Implement next permutation, which rearranges numbers into the lexicographically next greater permutation of numbers.
>
> If such arrangement is not possible, it must rearrange it as the lowest possible order (ie, sorted in ascending order).
>
> The replacement must be in-place, do not allocate extra memory.
>
> Here are some examples. Inputs are in the left-hand column and its corresponding outputs are in the right-hand column.
> 1,2,3 → 1,3,2
> 3,2,1 → 1,2,3
> 1,1,5 → 1,5,1

给定一个序列，求下一个排列形式（按字典序）。例如一个集合`{1, 2, 3}`，它的全排列有6种，按字典顺序：
```
1 2 3
1 3 2
2 1 3
2 3 1
3 1 2
3 2 1
```
如果给定序列`1 3 2`，那么下一个排列就是`2 1 3`，如果给定最后一个排列`3 2 1`，应该返回第一个排列`1 2 3`。要求空间复杂度`O(1)`。也就是说不能开新数组，需要inplace进行替换。

## 分析
搞清楚排列数的规律，可以用以下算法完成：

1. 从右向左扫描数组，找到第一个破坏升序(从右向左升序)规律的下标`pivot`。下一个排列不需要改变pivot左边的序列(想想为什么)。如果找不到pivot，也就是说数组整体是倒序了，那说明是最后一个排列，翻转成第一个排列就好了。
2. 这个时候我们知道要重新排列pivot右边的序列，这个序列（不包括pivot）是从左到右降序的。下一个排列在pivot位置上的数，应该是右边序列中比pivot上的数大的最小的数(想想为什么)。因此我们再次从右向左扫描数组（也可以二分查找），找到第一个比pivot大的数，交换它和pivot上的数。
3. 这时候，pivot位置右侧的序列仍然是降序的，我们翻转这个序列（变成升序的），这时候数组中的值就构成了下一个排列。

这个算法的时间复杂度是`O(n)`，空间复杂度`O(1)`。

## 代码

### Python
```python
class Solution(object):
    def nextPermutation(self, nums):
        """
        :type nums: List[int]
        :rtype: void Do not return anything, modify nums in-place instead.
        """
        pivot = -1
        for i in xrange(len(nums) - 1, 0, -1):
            if nums[i] > nums[i - 1]:
                pivot = i - 1
                break

        if pivot >= 0:
            for i in xrange(len(nums) - 1, 0, -1):
                if nums[i] > nums[pivot]:
                    nums[pivot], nums[i] = nums[i], nums[pivot]
                    break

        self.reverse(nums, pivot + 1, len(nums) - 1)

    def reverse(self, nums, i, j):
        if i >= j:
            return
        t = (j - i + 1) / 2
        for k in xrange(t):
            nums[i + k], nums[j - k] = nums[j - k], nums[i + k]  # swap
```
