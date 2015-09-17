title: Leetcode解题-Interleaving String
date: 2015-09-17 13:56:59
tags: [Leetcode, 动态规划]
categories: [编程题]
---

## 描述
> Given s1, s2, s3, find whether s3 is formed by the interleaving of s1 and s2.
>
> For example,
> Given:
> s1 = "aabcc",
> s2 = "dbbca",
>
> When s3 = "aadbbcbcac", return true.
> When s3 = "aadbbbaccc", return false.

## 分析
二维动态规划的思路，令`dp[i][j]`表示`s3的前i + j个字符是否可以由s1的前i个和s2的前j个字符交织组成`，显然有`dp[0][0] = True`，而`dp[0][j]`和`dp[i][0]`可以很容易预先填充，然后对于`dp[i][j]`，有递推公式

    dp[i][j] = (dp[i - 1][j] and s1[i - 1] == s3[i + j - 1]) or \
                (dp[i][j - 1] and s2[j - 1] == s3[i + j - 1])



## 代码
### Python
```python
class Solution(object):
    def isInterleave(self, s1, s2, s3):
        """
        :type s1: str
        :type s2: str
        :type s3: str
        :rtype: bool
        """
        n1 = len(s1)
        n2 = len(s2)
        if len(s3) != n1 + n2:
            return False
        dp = [[False] * (n2 + 1) for i in xrange(n1 + 1)]
        dp[0][0] = True
        for i in xrange(1, n1 + 1):
            dp[i][0] = dp[i - 1][0] and s1[i - 1] == s3[i - 1]
            if not dp[i][0]:
                break
        for j in xrange(1, n2 + 1):
            dp[0][j] = dp[0][j - 1] and s2[j - 1] == s3[j - 1]
            if not dp[0][j]:
                break

        for i in xrange(1, n1 + 1):
            for j in xrange(1, n2 + 1):
                if dp[i - 1][j] and s1[i - 1] == s3[i + j - 1]:
                    dp[i][j] = True
                if dp[i][j - 1] and s2[j - 1] == s3[i + j - 1]:
                    dp[i][j] = True
        return dp[n1][n2]
```
