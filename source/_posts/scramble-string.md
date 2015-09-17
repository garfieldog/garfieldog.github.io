title: Leetcode解题-Scramble String
date: 2015-09-17 14:51:45
tags: [Leetcode, 动态规划]
categories: [编程题]
---

## 描述
> Given a string s1, we may represent it as a binary tree by partitioning it to two non-empty substrings recursively.
>
> Below is one possible representation of s1 = "great":
>
>     great
>    /    \
>   gr    eat
>  / \    /  \
> g   r  e   at
>            / \
>           a   t
> To scramble the string, we may choose any non-leaf node and swap its two children.
>
> For example, if we choose the node "gr" and swap its two children, it produces a scrambled string "rgeat".
>
>     rgeat
>    /    \
>   rg    eat
>  / \    /  \
> r   g  e   at
>            / \
>           a   t
> We say that "rgeat" is a scrambled string of "great".
>
> Similarly, if we continue to swap the children of nodes "eat" and "at", it produces a scrambled string "rgtae".
>
>     rgtae
>    /    \
>   rg    tae
>  / \    /  \
> r   g  ta  e
>        / \
>       t   a
> We say that "rgtae" is a scrambled string of "great".
>
> Given two strings s1 and s2 of the same length, determine if s2 is a scrambled string of s1.

## 分析

这道题我已经弃疗了，三维动态规划，正确解摆在面前也费劲。参考[这里][1]。

有一个递归的解写起来比较容易，但是会超时。


## 代码
### 动态规划
```python
class Solution(object):
    def isScramble(self, s1, s2):
        """
        :type s1: str
        :type s2: str
        :rtype: bool
        """
        if len(s1) != len(s2):
            return False
        n = len(s1)
        dp = [[[False] * n for i in xrange(n)] for j in xrange(n + 1)]
        for i in xrange(n):
            for j in xrange(n):
                dp[1][i][j] = s1[i] == s2[j]

        for z in xrange(1, n + 1):
            for i in xrange(n - z + 1):
                for j in xrange(n - z + 1):
                    for k in xrange(1, z):
                        if (dp[k][i][j] and dp[z - k][i + k][j + k]) or \
                                (dp[k][i][j + z - k] and dp[z - k][i + k][j]):
                            dp[z][i][j] = True
                            break
        return dp[n][0][0]
```

### 递归（超时）
```python
class Solution(object):
    def isScramble(self, s1, s2):
        """
        :type s1: str
        :type s2: str
        :rtype: bool
        """
        if len(s1) != len(s2):
            return False
        n = len(s1)
        if s1 == s2:
            return True
        for i in xrange(1, n):
            if self.isScramble(s1[:i], s2[:i]) and \
                    self.isScramble(s1[i:], s2[i:]):
                return True
            if self.isScramble(s1[:i], s2[-i:]) and \
                    self.isScramble(s1[i:], s2[:-i]):
                return True
        return False
```

[1]: http://www.acmerblog.com/leetcode-solution-scramble-string-6224.html
