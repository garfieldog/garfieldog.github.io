title: Leetcode解题-N Queens
date: 2015-09-15 16:28:17
tags: [Leetcode, 回溯法, DFS]
categories: [编程题]
---

## 描述
> ![n-queens](/images/n-queens.png)
>
> Given an integer n, return all distinct solutions to the n-queens puzzle.
>
> Each solution contains a distinct board configuration of the n-queens' placement, where 'Q' and '.' both indicate a queen and an empty space respectively.
>
> For example,
> There exist two distinct solutions to the 4-queens puzzle:
>
> [
>  [".Q..",  // Solution 1
>   "...Q",
>   "Q...",
>   "..Q."],
>
>  ["..Q.",  // Solution 2
>   "Q...",
>   "...Q",
>   ".Q.."]
> ]

## 分析
这道题非常经典，最基础的做法就是DFS回溯。还有很多优化加速的方法，比如对角线缓存法。

## 代码
### 回溯
```python
class Solution(object):
    def check(self, path, y):
        j = len(path)
        for i, x in enumerate(path):
            if x == y or y - j == x - i or y + j == x + i:
                return False
        return True

    def dfs(self, n, path, rs):
        if n == len(path):
            rs.append(path[:])
            return
        for i in xrange(n):
            if self.check(path, i):
                path.append(i)
                self.dfs(n, path, rs)
                path.pop()

    def listToMaze(self, lst):
        rs = []
        n = len(lst)
        for x in lst:
            rs.append('.' * x + 'Q' + '.' * (n - x - 1))
        return rs

    def solveNQueens(self, n):
        """
        :type n: int
        :rtype: List[List[str]]
        """
        if n == 0:
            return 0
        rs = []
        path = []
        self.dfs(n, path, rs)
        return [self.listToMaze(x) for x in rs]
```

### 缓存对角线加速
```python
class Solution(object):
    def dfs(self, n, path, rs, diag1, diag2, visited):
        if n == len(path):
            rs.append(path[:])
            return
        x = len(path)
        for y in xrange(n):
            if not visited[y] and not diag1[x + y] and not diag2[x - y + n - 1]:
                path.append(y)
                visited[y] = True
                diag1[x + y] = True
                diag2[x - y + n - 1] = True
                self.dfs(n, path, rs, diag1, diag2, visited)
                visited[y] = False
                diag1[x + y] = False
                diag2[x - y + n - 1] = False
                path.pop()

    def listToMaze(self, lst):
        rs = []
        n = len(lst)
        for x in lst:
            rs.append('.' * x + 'Q' + '.' * (n - x - 1))
        return rs

    def solveNQueens(self, n):
        """
        :type n: int
        :rtype: List[List[str]]
        """
        if n == 0:
            return 0
        diag1 = [False] * (2 * n - 1)
        diag2 = [False] * (2 * n - 1)
        visited = [False] * n
        rs = []
        path = []
        self.dfs(n, path, rs, diag1, diag2, visited)
        return [self.listToMaze(x) for x in rs]
```
