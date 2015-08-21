title: Leetcode解题-4Sum
date: 2015-08-21 09:56:30
tags: [Leetcode, Array, 两指针, 哈希表]
categories: [编程题]
---

## 描述

> Given an array S of n integers, are there elements a, b, c, and d in S such that a + b + c + d = target? Find all unique quadruplets in the array which gives the sum of target.
>
> Note:
> Elements in a quadruplet (a,b,c,d) must be in non-descending order. (ie, a ≤ b ≤ c ≤ d)
> The solution set must not contain duplicate quadruplets.
> For example, given array S = {1 0 -1 0 -2 2}, and target = 0.
>
> A solution set is:
> (-1,  0, 0, 1)
> (-2, -1, 1, 2)
> (-2,  0, 0, 2)

## 分析

和[3Sum][1]可以用一样的两指针夹逼解法，时间复杂度`O(n^3)`，空间复杂度O(1)。还可以用空间换时间，用一个哈希表去缓存两数之和，时间复杂度平均降到`O(n^2)`，最坏`O(n^4)`(即所有元素都相等的时候)，空间复杂度`O(n)`。

## 代码

### 两指针法
```python
class Solution:
    # @return a list of lists of length 4, [[val1,val2,val3,val4]]
    def fourSum(self, nums, target):
        nums.sort()
        rs = set()
        for i in xrange(len(nums) - 3):
            for j in xrange(i + 1, len(nums) - 2):
                k = j + 1
                r = len(nums) - 1
                while k < r:
                    s = nums[i] + nums[j] + nums[k] + nums[r]
                    if s == target:
                        rs.add((nums[i], nums[j], nums[k], nums[r]))
                        k += 1
                        r -= 1
                    elif s > target:
                        r -= 1
                    else:
                        k += 1
        return [list(x) for x in rs]
```

### 哈希表加速
```python
class Solution:
    # @return a list of lists of length 4, [[val1,val2,val3,val4]]
    def fourSum(self, nums, target):
        nums.sort()
        rs = set()
        cache = {}
        for i in xrange(len(nums) - 1):
            for j in xrange(i + 1, len(nums)):
                cache.setdefault(nums[i] + nums[j], []).append((i, j))
        for i in xrange(len(nums) - 1):
            for j in xrange(i + 1, len(nums)):
                for k, r in cache.get(target - nums[i] - nums[j], []):
                    if j < k:  # notice: think about this condition
                        rs.add((nums[i], nums[j], nums[k], nums[r]))
        return [list(x) for x in rs]
```

[1]: /2015/08/20/3-sum/

