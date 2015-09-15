title: Leetcode解题-N Queens II
date: 2015-09-15 17:07:53
tags: [Leetcode, 回溯法, DFS]
categories: [编程题]
---

## 描述
> Follow up for N-Queens problem.
>
> Now, instead outputting board configurations, return the total number of distinct solutions.

## 分析
跟[上一题][1]其实完全一样，不用维护路径，只用一个全局变量计数就可以了。

## 代码
### Python
```python
class Solution(object):
    count = 0

    def dfs(self, n, depth, diag1, diag2, visited):
        if n == depth:
            self.count += 1
            return
        x = depth
        for y in xrange(n):
            if not visited[y] and not diag1[x + y] and not diag2[x - y + n - 1]:
                visited[y] = True
                diag1[x + y] = True
                diag2[x - y + n - 1] = True
                self.dfs(n, depth + 1, diag1, diag2, visited)
                visited[y] = False
                diag1[x + y] = False
                diag2[x - y + n - 1] = False

    def totalNQueens(self, n):
        """
        :type n: int
        :rtype: int
        """
        if n == 0:
            return 0
        diag1 = [False] * (2 * n - 1)
        diag2 = [False] * (2 * n - 1)
        visited = [False] * n
        self.dfs(n, 0, diag1, diag2, visited)
        return self.count
```

[1]: /2015/09/15/n-queens/
