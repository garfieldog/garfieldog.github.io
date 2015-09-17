title: Leetcode解题-Minimum Path Sum
date: 2015-09-17 15:55:30
tags: [Leetcode, 动态规划]
categories: [编程题]
---

## 描述
> Given a m x n grid filled with non-negative numbers, find a path from top left to bottom right which minimizes the sum of all numbers along its path.
>
> Note: You can only move either down or right at any point in time.

## 分析
终于来了道简单点的找点自信，普通二维动态规划，`dp[i][j]`代表以`(i, j)`为终点的路径的最小长度，则有`dp[i][j] = min(dp[i - 1][j], dp[i][j - 1]) + grid[i][j]`，很容易转化为一维空间。时间`O(mn)`，空间`O(n)`。

## 代码
### Python
```python
class Solution(object):
    def minPathSum(self, grid):
        """
        :type grid: List[List[int]]
        :rtype: int
        """
        m = len(grid)
        n = len(grid[0])
        dp = [0] * (n + 1)
        for i in xrange(1, n + 1):
            dp[i] = dp[i - 1] + grid[0][i - 1]

        dp[0] = float('inf')
        for i in xrange(1, m):
            for j in xrange(1, n + 1):
                dp[j] = min(dp[j], dp[j - 1]) + grid[i][j - 1]
        return dp[n]
```
