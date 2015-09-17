title: Leetcode解题-Word Break
date: 2015-09-17 19:16:38
tags: [Leetcode, 动态规划]
categories: [编程题]
---

## 描述
> Given a string s and a dictionary of words dict, determine if s can be segmented into a space-separated sequence of one or more dictionary words.
>
> For example, given
> s = "leetcode",
> dict = ["leet", "code"].
>
> Return true because "leetcode" can be segmented as "leet code".

## 分析
一维动态规划，令`dp[i]`表示前i个字符构成的字符串是否可以被分词，则`dp[i] = any(dp[j] && s[j:i] in wordDict), 0 <= j < i`。

## 代码
### Python
```python
class Solution(object):
    def wordBreak(self, s, wordDict):
        """
        :type s: str
        :type wordDict: Set[str]
        :rtype: bool
        """
        n = len(s)
        dp = [False] * (n + 1)
        dp[0] = True
        for i in xrange(1, n + 1):
            for j in xrange(i):
                if dp[j] and s[j: i] in wordDict:
                    dp[i] = True
                    break
        return dp[n]
```
