title: Leetcode解题-Palindrome Partitioning II
date: 2015-09-15 14:00:12
tags: [Leetcode, String, 动态规划]
categories: [编程题]
---

## 描述
> Given a string s, partition s such that every substring of the partition is a palindrome.
>
> Return the minimum cuts needed for a palindrome partitioning of s.
>
> For example, given s = "aab",
> Return 1 since the palindrome partitioning ["aa","b"] could be produced using 1 cut.

## 分析
是[上一题][1]的升级版，要求找到最小划分。
采用动态规划法，设`f(i, j)`为`s[i:j+1]`之间最小的切割数，则有`f(i, j) = min(f(i, k) + f(k + 1, j)), i<=k<=j`。可以把这个递推条件转化为一维的，另`dp[i]`表示`s[0:i]`的最小切割数，则`dp[i] = min(dp[j] + 1), 0<=j<i`。 这个有点tricky，这样来想`dp[j]`代表了前j个字符的最小割数，而`dp[i]`(i > j)的就可以拆分成这些情况：

    第i个字符自成一个回文，加上前i-1个字符的最小割数dp[i - 1] + 1
    第i-1, i两个个字符成一个回文，加上前i-2个字符的最小割数dp[i - 2] + 1
    ...
    第2, 3, ..., i个字符成一个回文，加上前1个字符的最小割数dp[1] + 1
    前i个字符成一个回文，这个时候最小割数应该是0，因为不用切割，为了统一形式，我们令dp[0] = -1, 则可以写作dp[0] + 1

所有这些情况的最小值就是`dp[i]`的值。


## 代码
### Python
```python
class Solution(object):
    def minCut(self, s):
        """
        :type s: str
        :rtype: int
        """
        n = len(s)
        if n == 0:
            return 0

        isPal = [[False] * n for i in xrange(n)]
        for i in xrange(n - 1, -1, -1):
            for j in xrange(i, n):
                if (i + 1 > j - 1 or isPal[i + 1][j - 1]) and s[i] == s[j]:
                    isPal[i][j] = True

        dp = [float('inf')] * (n + 1)
        dp[0] = -1
        for i in xrange(1, n + 1):
            for j in xrange(i - 1, -1, -1):
                if isPal[j][i - 1]:
                    dp[i] = min(dp[i], dp[j] + 1)
        return dp[n]
```

[1]: /2015/09/15/palindrome-partitioning/
