title: Leetcode解题-Palindrome Partitioning
date: 2015-09-15 09:50:08
tags: [Leetcode, String, DFS, 回溯法]
categories: [编程题]
---

## 描述
> Given a string s, partition s such that every substring of the partition is a palindrome.
>
> Return all possible palindrome partitioning of s.
>
> For example, given s = "aab",
> Return
>
>   [
>     ["aa","b"],
>     ["a","a","b"]
>   ]

## 分析
一个长度为`n`的字符串有`n - 1`个空隙，每个空隙可以选择切还是不切，所以共有`2 ^ (n - 1)`种划分。使用回溯法，时间复杂度`O(n*2^n)`，空间`O(n)`。

## 代码
### Python
```python
class Solution(object):
    def isPalindrome(self, s, start, end):
        while start <= end:
            if s[start] != s[end]:
                return False
            start += 1
            end -= 1
        return True

    def dfs(self, s, path, rs, start):
        n = len(s)
        if start == n:
            rs.append(path[:])
            return

        for i in xrange(start, n):
            if self.isPalindrome(s, start, i):
                path.append(s[start: i + 1])
                self.dfs(s, path, rs, i + 1)
                path.pop()

    def partition(self, s):
        """
        :type s: str
        :rtype: List[List[str]]
        """
        n = len(s)
        if n == 0:
            return [[]]
        path = []
        rs = []
        self.dfs(s, path, rs, 0)
        return rs
```
