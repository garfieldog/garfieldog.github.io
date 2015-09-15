title: Leetcode解题-Unique Paths
date: 2015-09-15 15:10:50
tags: [Leetcode, 动态规划, Maze, Math]
categories: [编程题]
---

## 描述
> A robot is located at the top-left corner of a m x n grid (marked 'Start' in the diagram below).
>
> The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).
>
> How many possible unique paths are there?
>
> ![robot.png](/images/robot.png)
> Above is a 3 x 7 grid. How many possible unique paths are there?
>
> Note: m and n will be at most 100.

## 分析
这个很容易看出来动态规划的解。用`dp[i][j]`表示从坐标`(i, j)`到终点坐标有多少种走法，可知`dp[i][j] = dp[i+1][j] + dp[i][j+1]`。从下到上，从右到左扫表即可。时间`O(mn)`，空间`O(mn)`。

其实，还有一个更漂亮的解，从`(0, 0)`到`(m, n)`需要走`m + n - 2`步，而其中有`m - 1`步是向下的，`n - 1`步是向右的。可知解为 $ \binom{ m + n - 2 }{ m - 1 } $

## 代码
### 动态规划
```python
class Solution(object):
    def uniquePaths(self, m, n):
        """
        :type m: int
        :type n: int
        :rtype: int
        """
        if m == 0 or n == 0:
            return 0
        dp = [[0] * n for i in xrange(m)]
        for i in xrange(m):
            dp[i][n - 1] = 1
        for j in xrange(n):
            dp[m - 1][j] = 1

        for i in xrange(m - 2, -1, -1):
            for j in xrange(n - 2, -1, -1):
                dp[i][j] = dp[i + 1][j] + dp[i][j + 1]
        return dp[0][0]
```

### 组合数
```python
import math


class Solution(object):
    def nCr(self, n, r):
        f = math.factorial
        return f(n) / f(n - r) / f(r)

    def uniquePaths(self, m, n):
        """
        :type m: int
        :type n: int
        :rtype: int
        """
        if m == 0 or n == 0:
            return 0
        return self.nCr(m + n - 2, m - 1)
```
