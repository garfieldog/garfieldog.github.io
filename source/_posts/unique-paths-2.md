title: Leetcode解题-Unique Paths II
date: 2015-09-15 15:28:07
tags: [Leetcode, DFS, Maze, 动态规划]
categories: [编程题]
---

## 描述
> Follow up for "Unique Paths":
>
> Now consider if some obstacles are added to the grids. How many unique paths would there be?
>
> An obstacle and empty space is marked as 1 and 0 respectively in the grid.
>
> For example,
> There is one obstacle in the middle of a 3x3 grid as illustrated below.
>
> [
>   [0,0,0],
>   [0,1,0],
>   [0,0,0]
> ]
> The total number of unique paths is 2.
>
> Note: m and n will be at most 100.

## 分析
这次有障碍了，就不能简单用组合数解了。可以DFS，但是容易超时，可以把[上一题][1]的动态规划改一下，注意有障碍物的格子走法要处理为0。

## 代码
### DFS(超时)
```python
class Solution(object):
    count = 0

    def uniquePathsWithObstacles(self, obstacleGrid):
        """
        :type obstacleGrid: List[List[int]]
        :rtype: int
        """

        def dfs(x, y):
            if x == m - 1 and y == n - 1:
                self.count += 1
                return
            if x + 1 < m and A[x + 1][y] == 0:
                dfs(x + 1, y)
            if y + 1 < n and A[x][y + 1] == 0:
                dfs(x, y + 1)

        A = obstacleGrid
        m = len(A)
        if m == 0:
            return 0
        n = len(A[0])
        if n == 0:
            return 0
        dfs(0, 0)
        return self.count
```

### 动态规划
```python
class Solution(object):
    def uniquePathsWithObstacles(self, obstacleGrid):
        """
        :type obstacleGrid: List[List[int]]
        :rtype: int
        """

        A = obstacleGrid
        m = len(A)
        if m == 0:
            return 0
        n = len(A[0])
        if n == 0:
            return 0
        dp = [[0] * n for i in xrange(m)]
        dp[m - 1][n - 1] = 1 if A[m - 1][n - 1] == 0 else 0
        for i in xrange(m - 2, -1, -1):
            if A[i][n - 1] == 0 and dp[i + 1][n - 1] > 0:
                dp[i][n - 1] = 1
        for j in xrange(n - 2, -1, -1):
            if A[m - 1][j] == 0 and dp[m - 1][j + 1] > 0:
                dp[m - 1][j] = 1

        for i in xrange(m - 2, -1, -1):
            for j in xrange(n - 2, -1, -1):
                if A[i][j] == 0:
                    dp[i][j] = dp[i + 1][j] + dp[i][j + 1]
                else:
                    dp[i][j] = 0
        return dp[0][0]
```

[1]: /2015/09/15/unique-paths/
