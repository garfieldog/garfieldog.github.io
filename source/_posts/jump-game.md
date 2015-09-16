title: Leetcode解题-Jump Game
date: 2015-09-16 14:30:34
tags: [Leetcode, 贪心法]
categories: [编程题]
---

## 描述
> Given an array of non-negative integers, you are initially positioned at the first index of the array.
>
> Each element in the array represents your maximum jump length at that position.
>
> Determine if you are able to reach the last index.
>
> For example:
> A = [2,3,1,1,4], return true.
>
> A = [3,2,1,0,4], return false.

## 分析
DFS固然是可以，但其实可以只保留一条路径（就是每次都选可选范围内下一个最大的步数，反证法可证如果有解，这样肯定能找到一个解），其他路径都被剪枝，这样一来就满足了贪心法的条件。

## 代码
### 迭代
```python
class Solution(object):
    def canJump(self, nums):
        """
        :type nums: List[int]
        :rtype: bool
        """
        n = len(nums)
        step = nums[0]
        for i in xrange(1, n):
            if step > 0:
                step -= 1
                step = max(step, nums[i])
            else:
                return False
        return True
```
