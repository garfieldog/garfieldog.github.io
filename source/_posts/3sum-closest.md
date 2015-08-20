title: Leetcode解题-3Sum Closest
date: 2015-08-20 13:33:43
tags: [Leetcode, Array]
categories: [编程题]
---

## 描述

> Given an array S of n integers, find three integers in S such that the sum is closest to a given number, target. Return the sum of the three integers. You may assume that each input would have exactly one solution.
>
> For example, given array S = {-1 2 1 -4}, and target = 1.
>
> The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).

和上一题[3Sum][1]基本设定一样，不过这次要求找到与`target`最相近的三数之和。返回和的值即可，不需要给出所有组合。

## 分析
沿用[3Sum][1]的解法，用一个变量维护当前最小绝对差值即可。时间复杂度`O(n^2)`，空间复杂度`O(1)`。

## 代码

### Python
```python
class Solution:
    def threeSumClosest(self, nums, target):
        nums.sort()
        ret = None
        cur_diff = None
        for i in xrange(len(nums) - 2):
            j = i + 1
            k = len(nums) - 1
            while j < k:
                s = nums[i] + nums[j] + nums[k]
                if s == target:
                    return target
                elif s > target:
                    k -= 1
                else:
                    j += 1
                if cur_diff is None or cur_diff > abs(s - target):
                    cur_diff = abs(s - target)
                    ret = s
        return ret
```


[1]: /2015/08/20/3-sum/

