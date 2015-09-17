title: Leetcode解题-Distinct Subsequences
date: 2015-09-17 17:39:25
tags: [Leetcode, 动态规划]
categories: [编程题]
---

## 描述
> Given a string S and a string T, count the number of distinct subsequences of T in S.
>
> A subsequence of a string is a new string which is formed from the original string by deleting some (can be none) of the characters without disturbing the relative positions of the remaining characters. (ie, "ACE" is a subsequence of "ABCDE" while "AEC" is not).
>
> Here is an example:
> S = "rabbbit", T = "rabbit"
>
> Return 3.

## 分析
令`dp[i][j]`表示t的前j个字符在s的前i个字符组成的字符串中的subsequences个数，如果`s[i] == t[j]`，则可以选择用t[j]或者不用t[j]，`dp[i][j] = dp[i - 1][j] + dp[i - 1][j - 1]`，若`s[i] != t[j]`，则显然`dp[i][j] = dp[i - 1][j]`。可以把dp数组降到一维。

## 代码
### Python
```python
class Solution(object):
    def numDistinct(self, s, t):
        """
        :type s: str
        :type t: str
        :rtype: int
        """
        m = len(s)
        n = len(t)
        dp = [0] * (n + 1)
        dp[0] = 1
        for i in xrange(m):
            for j in xrange(n, 0, -1):
                if s[i] == t[j - 1]:
                    dp[j] += dp[j - 1]
        return dp[n]
```
