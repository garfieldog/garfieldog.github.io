title: Leetcode解题-Combinations
date: 2015-09-14 14:48:12
tags: [Leetcode, DFS]
categories: [编程题]
---

## 描述
> Given two integers n and k, return all possible combinations of k numbers out of 1 ... n.
>
> For example,
> If n = 4 and k = 2, a solution is:
>
> [
>   [2,4],
>   [3,4],
>   [2,3],
>   [1,2],
>   [1,3],
>   [1,4],
> ]

## 分析
典型的回溯法。时间`O(n!)`，空间`O(n)`。注意组合数和排列数不同，[1, 2] 和[2, 1]是同一个组合，不要加重了。

## 代码
### 递归
```python
class Solution(object):
    def dfs(self, n, k, path, rs):
        if len(path) == k:
            rs.append(path[:])
            return
        for i in xrange(1, n + 1):
            if not path or path[-1] < i:
                path.append(i)
                self.dfs(n, k, path, rs)
                path.pop()

    def combine(self, n, k):
        """
        :type n: int
        :type k: int
        :rtype: List[List[int]]
        """
        path = []
        rs = []
        self.dfs(n, k, path, rs)
        return rs
```

### 递归（稍作优化）
```python
class Solution(object):
    def dfs(self, n, k, path, rs):
        if len(path) == k:
            rs.append(path[:])
            return
        start = path[-1] + 1 if path else 1
        for i in xrange(start, n + 1):
            path.append(i)
            self.dfs(n, k, path, rs)
            path.pop()

    def combine(self, n, k):
        """
        :type n: int
        :type k: int
        :rtype: List[List[int]]
        """
        path = []
        rs = []
        self.dfs(n, k, path, rs)
        return rs
```
