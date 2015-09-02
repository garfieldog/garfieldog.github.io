title: Leetcode解题-Regular Expression Matching
date: 2015-09-01 18:30:11
tags: [Leetcode, String, 动态规划, 正则表达式]
categories: [编程题]
---

## 描述
> Implement regular expression matching with support for '.' and '\*'.
>
> '.' Matches any single character.
> '\*' Matches zero or more of the preceding element.
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
> isMatch("aa", "a\*") → true
> isMatch("aa", ".\*") → true
> isMatch("ab", ".\*") → true
> isMatch("aab", "c\*a\*b") → true

## 分析
有一定难度，主要是判断`*`。可以采取[递归法][1]或[动态规划][2]。当然，转换为DFA自动机然后做也是没问题的，但实现难度就要更大一些。

### TBD
算法分析参考上面给的两篇文章链接。具体分析有点复杂，先留空，刷完题再补。

## 代码

### 递归法
Leetcode上提交会超时
```python
END = '\001'


class Solution(object):
    def isMatchR(self, s, i, p, j):
        if p[j] == END:
            return s[i] == END

        if p[j + 1] != '*':
            return (p[j] == s[i] or (p[j] == '.' and s[i] != END)) \
                and self.isMatchR(s, i + 1, p, j + 1)
        # p[j] == '*'
        while(p[j] == s[i] or (p[j] == '.' and s[i] != END)):
            if self.isMatchR(s, i, p, j + 2):
                return True
            i += 1

        return self.isMatchR(s, i, p, j + 2)

    def isMatch(self, s, p):
        """
        :type s: str
        :type p: str
        :rtype: bool
        """
        s += END
        p += END
        return self.isMatchR(s, 0, p, 0)
```

### 动态规划
```python
class Solution(object):
    def isMatchChar(self, a, b):
        return a == b or b == '.'

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
        # fisrt row, s == ''
        for i in xrange(1, m + 1):
            if p[i - 1] == '*':
                if i > 1:
                    dp[0][i] = dp[0][i - 2]
            # otherwise leave dp[0][i] = False
        for i in xrange(1, n + 1):
            # leave dp[i][0] = False for i > 0
            for j in xrange(1, m + 1):
                if p[j - 1] == '*':
                    # j must > 1
                    dp[i][j] = dp[i][j - 1] or dp[i][j - 2] or \
                        (dp[i - 1][j] and self.isMatchChar(s[i - 1], p[j - 2]))
                else:
                    dp[i][j] = dp[i - 1][j - 1] and self.isMatchChar(s[i - 1], p[j - 1])
        return dp[n][m]
```

[1]: http://articles.leetcode.com/2011/09/regular-expression-matching.html
[2]: http://www.cnblogs.com/flowerkzj/p/3726667.html
