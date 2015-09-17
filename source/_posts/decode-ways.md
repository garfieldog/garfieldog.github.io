title: Leetcode解题-Decode Ways
date: 2015-09-17 16:32:33
tags: [Leetcode, 动态规划, Decoding]
categories: [编程题]
---

## 描述
> A message containing letters from A-Z is being encoded to numbers using the following mapping:
>
> 'A' -> 1
> 'B' -> 2
> ...
> 'Z' -> 26
> Given an encoded message containing digits, determine the total number of ways to decode it.
>
> For example,
> Given encoded message "12", it could be decoded as "AB" (1 2) or "L" (12).
>
> The number of ways decoding "12" is 2.

## 分析
这道题乍一看让人想起了[Restore IP Addresses][1]，这道题用DFS肯定能做，但效率不高。简单观察一下就会发现动态规划的最优子结构。用`dp[i]`表示前i个字符解码方法数，则如果当前字符和前一个字符可以构成合法的两位数，则`dp[i] = dp[i - 1] + dp[i - 2]`，否则`dp[i] = dp[i - 1]`。 注意这道题的测试用例里有很多非法的`0`，处理这些非法值是比较麻烦的一点。

## 代码
### Python
```python
class Solution(object):
    def numDecodings(self, s):
        """
        :type s: str
        :rtype: int
        """
        if not s or s[0] == '0':
            return 0
        n = len(s)
        dp = [0] * (n + 1)
        dp[0] = dp[1] = 1
        for i in xrange(2, n + 1):
            if 9 < int(s[i - 2: i]) <= 26:
                dp[i] += dp[i - 2]
            if s[i - 1] != '0':
                dp[i] += dp[i - 1]
        return dp[n]
```

[1]: /2015/09/15/restore-ip-addresses/
