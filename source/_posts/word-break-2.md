title: Leetcode解题-Word Break II
date: 2015-09-17 19:29:06
tags: [Leetcode, 动态规划, DFS]
categories: [编程题]
---

## 描述
> Given a string s and a dictionary of words dict, add spaces in s to construct a sentence where each word is a valid dictionary word.
>
> Return all such possible sentences.
>
> For example, given
> s = "catsanddog",
> dict = ["cat", "cats", "and", "sand", "dog"].
>
> A solution is ["cats and dog", "cat sand dog"].

## 分析
在[Word Break][1]的基础上，要求返回所有可能的分词结果。我们用一个二维数组`A[i][j]`来表示`s[j:i]`是不是一个单词（注意下标是反的）。然后通过对`A`进行DFS我们可以还原所有的合法组合。理解了之后要写对还是不容易。

## 代码
### Python
```python
class Solution(object):
    def dfs(self, s, A, idx, path, rs):
        if idx == 0:
            rs.append(' '.join(path[::-1]))
            return
        for i in xrange(idx):
            if A[idx][i]:
                # s[i: idx] is a word
                path.append(s[i: idx])
                self.dfs(s, A, i, path, rs)
                path.pop()

    def wordBreak(self, s, wordDict):
        """
        :type s: str
        :type wordDict: Set[str]
        :rtype: List[str]
        """
        n = len(s)
        dp = [False] * (n + 1)
        dp[0] = True
        A = [[False] * n for i in xrange(n + 1)]
        for i in xrange(1, n + 1):
            for j in xrange(i - 1, -1, -1):
                if dp[j] and s[j: i] in wordDict:
                    dp[i] = True
                    A[i][j] = True
        if not dp[n]:
            return []
        rs = []
        path = []
        self.dfs(s, A, n, path, rs)
        return rs
```

[1]: /2015/09/17/word-break/
