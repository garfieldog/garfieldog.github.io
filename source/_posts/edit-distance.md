title: Leetcode解题-Edit Distance
date: 2015-09-17 16:13:19
tags: [Leetcode, 动态规划, String]
categories: [编程题]
---

## 描述
> Given two words word1 and word2, find the minimum number of steps required to convert word1 to word2. (each operation is counted as 1 step.)
>
> You have the following 3 operations permitted on a word:
>
> a) Insert a character
> b) Delete a character
> c) Replace a character

## 分析
`编辑距离`是一个很重要的文本相似度度量标准，比较经典，通常的解法都是二维动态规划。`dp[i][j]`代表word1中前i个字符和word2前j个字符的编辑距离，则有

    dp[i][j] = dp[i - 1][j - 1] (if word1[i] == word2[j])
    dp[i][j] = min(dp[i - 1][j], dp[i][j - 1], dp[i - 1][j - 1]) + 1 (otherwise)

## 代码
### Python
```python
class Solution(object):
    def minDistance(self, word1, word2):
        """
        :type word1: str
        :type word2: str
        :rtype: int
        """
        n1 = len(word1)
        n2 = len(word2)
        if word1 == word2:
            return 0
        dp = [[0] * (n2 + 1) for i in xrange(n1 + 1)]
        for i in xrange(1, n1 + 1):
            dp[i][0] = i
        for j in xrange(1, n2 + 1):
            dp[0][j] = j

        for i in xrange(1, n1 + 1):
            for j in xrange(1, n2 + 1):
                if word1[i - 1] == word2[j - 1]:
                    dp[i][j] = dp[i - 1][j - 1]
                else:
                    dp[i][j] = min(dp[i - 1][j], dp[i][j - 1], dp[i - 1][j - 1]) + 1
        return dp[n1][n2]
```
