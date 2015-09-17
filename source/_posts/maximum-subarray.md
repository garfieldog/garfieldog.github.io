title: Leetcode解题-Maximum Subarray
date: 2015-09-17 10:21:10
tags: [Leetcode, 动态规划]
categories: [编程题]
---

## 描述
> Find the contiguous subarray within an array (containing at least one number) which has the largest sum.
>
> For example, given the array [−2,1,−3,4,−1,2,1,−5,4],
> the contiguous subarray [4,−1,2,1] has the largest sum = 6.
>
> More practice:
> If you have figured out the O(n) solution, try coding another solution using the divide and conquer approach, which is more subtle.

## 分析
经典的教科书题，最大连续子序列。最简单的解是双重循环遍历数组下标，选择区间`[i..j]`比较加和，时间`O(n^3)`，必然超时。我们来寻找最优子结构，另`dp[i]`为`以nums[i]为结尾的子数组最大加和`，则`dp[i] = max(dp[i - 1], 0) + nums[i]`。一维动态规划，时间`O(n)`，空间`O(n)`。

## 代码
### Python
```python
class Solution(object):
    def maxSubArray(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        n = len(nums)
        dp = [0] * n
        dp[0] = nums[0]
        for i in xrange(1, n):
            dp[i] = max(0, dp[i - 1]) + nums[i]
        return max(dp)
```
