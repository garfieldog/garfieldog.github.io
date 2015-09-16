title: Leetcode解题-Generate Parentheses
date: 2015-09-16 09:43:31
tags: [Leetcode, 回溯法, DFS]
categories: [编程题]
---

## 描述
> Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.
>
> For example, given n = 3, a solution set is:
>
> "((()))", "(()())", "(())()", "()(())", "()()()"

## 分析
依然是熟悉的回溯法，不过这次我们需要一个额外的栈（其实一个整数变量就可以）来保证括号的匹配性。

## 代码
### Python
```python
class Solution(object):
    def dfs(self, n, n1, n2, stack, path, rs):
        if n == n1 and n == n2:
            rs.append(path[:])
            return

        if n1 < n:
            path.append('(')
            self.dfs(n, n1 + 1, n2, stack + 1, path, rs)
            path.pop()
        if n2 < n and stack > 0:
            path.append(')')
            self.dfs(n, n1, n2 + 1, stack - 1, path, rs)
            path.pop()

    def generateParenthesis(self, n):
        """
        :type n: int
        :rtype: List[str]
        """
        if n == 0:
            return []
        rs = []
        path = []
        self.dfs(n, 0, 0, 0, path, rs)
        return [''.join(x) for x in rs]
```
