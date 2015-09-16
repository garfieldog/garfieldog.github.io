title: Leetcode解题-Jump Game II
date: 2015-09-16 15:11:06
tags: [Leetcode, 贪心法]
categories: [编程题]
---

## 描述
> Given an array of non-negative integers, you are initially positioned at the first index of the array.
>
> Each element in the array represents your maximum jump length at that position.
>
> Your goal is to reach the last index in the minimum number of jumps.
>
> For example:
> Given array A = [2,3,1,1,4]
>
> The minimum number of jumps to reach the last index is 2. (Jump 1 step from index 0 to 1, then 3 steps to the last index.)

## 分析
[Jump Game][1]的后继问题，这次要求得出最小跳跃步数，我们用两个变量来分别记录`现在到达的位置`和`下一次最大能到达的未知`，遍历数组，如果下标超出`现在到达的位置`，则说明需要跳一步。比较巧妙，需要仔细推敲。

## 代码
### Python
```python
class Solution(object):
    def jump(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        n = len(nums)
        count = 0
        reach = 0
        next_reach = 0
        step = nums[0]
        if n <= 1:
            return 0
        for i in xrange(n):
            if step > 0:
                step -= 1
                step = max(step, nums[i])
            else:
                return -1

            if i > reach:
                reach = next_reach
                count += 1
            next_reach = max(next_reach, i + nums[i])
        return count
```

[1]: /2015/09/16/jump-game/
