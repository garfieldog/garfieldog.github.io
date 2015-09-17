title: Leetcode解题-Triangle
date: 2015-09-17 09:51:16
tags: [Leetcode, 动态规划]
categories: [编程题]
---

## 描述
> Given a triangle, find the minimum path sum from top to bottom. Each step you may move to adjacent numbers on the row below.
>
> For example, given the following triangle
> [
>      [2],
>     [3,4],
>    [6,5,7],
>   [4,1,8,3]
> ]
> The minimum path sum from top to bottom is 11 (i.e., 2 + 3 + 5 + 1 = 11).
>
> Note:
> Bonus point if you are able to do this using only O(n) extra space, where n is the total number of rows in the triangle.

## 分析
一道典型的动态规划题，我们用`dp[i][j]`表示`以root为头、triangle[i][j]为结束节点的最短路径长度`，则`dp[i][j] = min(dp[i - 1][j], dp[i - 1][j - 1]) + triangle[i][j]`。这个二维递推式可以用一个一维数组来完成，只要每一行都倒着填充就可以了。

## 代码
### Python
```python
class Solution(object):
    def minimumTotal(self, triangle):
        """
        :type triangle: List[List[int]]
        :rtype: int
        """
        n = len(triangle)
        dp = [float('inf')] * (n + 1)
        min_path = triangle[0][0]
        dp[1] = min_path
        for i in xrange(1, n):
            for j in xrange(i + 1, 0, -1):
                dp[j] = min(dp[j], dp[j - 1]) + triangle[i][j - 1]
        return min(dp)
```
