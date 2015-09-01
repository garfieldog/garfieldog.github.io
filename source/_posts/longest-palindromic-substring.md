title: Leetcode解题-Longest Palindromic Substring
date: 2015-08-31 19:15:48
tags: [Leetcode, String, Palindrome, 动态规划]
categories: [编程题]
---

## 描述
> Given a string S, find the longest palindromic substring in S. You may assume that the maximum length of S is 1000, and there exists one unique longest palindromic substring.

## 分析
如果暴力搜索，对每一个位置都进行两边扩张，时间复杂度为`O(n^2)`。进过观察发现判断从位置`i`到`j`之间的字符串是否为回文满足动态规划的最优子结构`f(i, j) = (s[j] == s[i]) and (j - i < 2 or f(i + 1, j - 1))`。所以可以使用一个二维数组来缓存子问题结果，时间复杂度`O(n^2)`，空间`O(n^2)`。

目前最优的解法是[Manacher][1]算法，通过一个精妙的构造省去了大量冗余的搜索。对于长回文字符串时间可以降到`O(n)`。

## 代码

### 暴力搜索
```python
class Solution(object):
    def longestPalindrome(self, s):
        """
        :type s: str
        :rtype: str
        """
        max_len = 0
        idx = -1
        n = len(s)
        for i in xrange(n):
            j = 1
            # search as center
            l = 1
            while i - j >= 0 and i + j < n and s[i - j] == s[i + j]:
                l += 2
                j += 1

            if l > max_len:
                max_len = l
                idx = i - (l - 1) / 2

            # search as left center
            if i + 1 < n and s[i] == s[i + 1]:
                l = 2
                j = 1
                while i - j >= 0 and i + 1 + j < n and s[i - j] == s[i + 1 + j]:
                    l += 2
                    j += 1
                if l > max_len:
                    max_len = l
                    idx = i - l / 2 + 1
        return s[idx: idx + max_len]
```

### 动态规划
在Leetcode上提交会超时
```python
class Solution(object):
    def longestPalindrome(self, s):
        """
        :type s: str
        :rtype: str
        """
        n = len(s)
        # matrix to store if s[i:j+1] is palindrome
        f = [[False] * n for i in xrange(n)]
        max_len = 0
        idx = -1
        for j in xrange(n):
            f[j][j] = True
            for i in xrange(j):
                f[i][j] = (s[j] == s[i]) and (j - i < 2 or f[i + 1][j - 1])
                if f[i][j] and (j - i + 1) > max_len:
                    max_len = j - i + 1
                    idx = i
        return s[idx: idx + max_len]
```

### Manacher算法
```python
class Solution(object):
    def preProcess(self, s):
        if not s:
            return '^$'
        rs = ['^']
        for c in s:
            rs.append('#')
            rs.append(c)
        rs.append('#$')
        return ''.join(rs)

    def longestPalindrome(self, s):
        """
        :type s: str
        :rtype: str
        """
        if not s:
            return s
        ns = self.preProcess(s)
        n = len(ns)
        p = [0] * n
        idx = 0
        mx = 0
        for i in xrange(1, n - 1):
            j = 2 * idx - i
            if i < mx:
                p[i] = min(mx - i, p[j])
            else:
                p[i] = 1

            while ns[i + p[i]] == ns[i - p[i]]:
                p[i] += 1

            if i + p[i] > mx:
                mx = i + p[i]
                idx = i

        max_len = 0
        max_idx = 0
        for i in xrange(1, n - 1):
            if p[i] > max_len:
                max_len = p[i]
                max_idx = i
        return s[(max_idx - max_len) / 2: (max_idx + max_len - 1) / 2]
```

[1]: http://articles.leetcode.com/2011/11/longest-palindromic-substring-part-ii.html
