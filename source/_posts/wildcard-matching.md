title: Leetcode解题-Wildcard Matching
date: 2015-09-02 12:20:18
tags: [Leetcode, String, 动态规划, 贪心法]
categories: [编程题]
---

## 描述
> Implement wildcard pattern matching with support for '?' and '\*'.
>
> '?' Matches any single character.
> '\*' Matches any sequence of characters (including the empty sequence).
>
> The matching should cover the entire input string (not partial).
>
> The function prototype should be:
> bool isMatch(const char \*s, const char \*p)
>
> Some examples:
> isMatch("aa","a") → false
> isMatch("aa","aa") → true
> isMatch("aaa","aa") → false
> isMatch("aa", "\*") → true
> isMatch("aa", "a\*") → true
> isMatch("ab", "?\*") → true
> isMatch("aab", "c\*a\*b") → false

## 分析
和[Regular Expression Matching][1]很像，但`*`的解释是不一样的，正则中`*`是匹配它前面一个字符出现0或多次，通配符中`*`可以匹配任意字符出现0或多次。

可以套用上一题的动态规划解法，时间空间都是`O(mn)`（其实空间可以降到`O(m)`），但这个解法在网站上提交会超时，有一个更有效率的迭代解法可以参考[这里][2]。这个解法的关键在于遇到`*`时进行`反贪心`( 就是首先考虑一个字符都不匹配的情况)匹配，如果失败则增加匹配字符数进行回溯。时间`O(mn)`，空间`O(1)`。

## 代码

### 动态规划
由于Leetcode测试用例中有非常长的串，该算法会判超时
```python
class Solution(object):
    def isMatchChar(self, a, b):
        return a == b or b == '?'

    def isMatch(self, s, p):
        """
        :type s: str
        :type p: str
        :rtype: bool
        """
        m = len(p)
        n = len(s)
        dp = [[False] * (m + 1) for i in xrange(n + 1)]
        dp[0][0] = True
        # first row, s == ''
        for i in xrange(1, m + 1):
            if p[i - 1] == '*':
                dp[0][i] = dp[0][i - 1]

        for i in xrange(1, n + 1):
            for j in xrange(1, m + 1):
                if p[j - 1] == '*':
                    dp[i][j] = dp[i][j - 1] or dp[i - 1][j]
                else:
                    dp[i][j] = dp[i - 1][j - 1] and self.isMatchChar(s[i - 1], p[j - 1])
        return dp[n][m]
```

### 递归
超时

```python
class Solution(object):
    def isMatchChar(self, a, b):
        return a == b or b == '?'

    def isMatchR(self, s, i, p, j):
        m, n = len(p), len(s)
        if j == m:
            return i == n

        if p[j] == '*':
            while j < m and p[j] == '*':
                j += 1
            if j == m:
                return True
            while i < n and not self.isMatchR(s, i, p, j):
                i += 1
            return i < n
        elif i == n:
            return j == m
        elif self.isMatchChar(s[i], p[j]):
            return self.isMatchR(s, i + 1, p, j + 1)
        else:
            return False

    def isMatch(self, s, p):
        """
        :type s: str
        :type p: str
        :rtype: bool
        """
        return self.isMatchR(s, 0, p, 0)
```

### 迭代
```python
class Solution(object):
    def isMatchChar(self, a, b):
        return a == b or b == '?'

    def isMatch(self, s, p):
        """
        :type s: str
        :type p: str
        :rtype: bool
        """
        m = len(p)
        n = len(s)
        i = j = 0
        star = -1
        si = 0
        while i < n:
            if j < m and self.isMatchChar(s[i], p[j]):
                i += 1
                j += 1
            elif j < m and p[j] == '*':
                si = i  # store matched position for s
                star = j  # store star position
                j += 1
            # p[j] != '*' and s[i] is not mathced to p[j]
            elif star >= 0:
                # has star, consume one char in s, and search back
                j = star + 1
                si += 1
                i = si
            else:
                # no star and not match
                return False
        while j < m and p[j] == '*':
            j += 1
        return j == m
```

[1]: /2015/09/01/regular-expression-matching/
[2]: http://www.cnblogs.com/zuoyuan/p/3781872.html
