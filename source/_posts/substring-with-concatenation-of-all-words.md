title: Leetcode解题-Substring with Concatenation of All Words
date: 2015-09-18 16:29:19
tags: [Leetcode, String]
categories: [编程题]
---

## 描述
> You are given a string, s, and a list of words, words, that are all of the same length. Find all starting indices of substring(s) in s that is a concatenation of each word in words exactly once and without any intervening characters.
>
> For example, given:
> s: "barfoothefoobarman"
> words: ["foo", "bar"]
>
> You should return the indices: [0,9].
> (order does not matter).

## 分析
这是一道细节实现题，方法是在对`s`每一个下标`i`，检查从`i`开始的`len(words)`个单词是不是刚好是`words`里的单词。

## 代码
### Python
```python
class Solution(object):
    def findSubstring(self, s, words):
        """
        :type s: str
        :type words: List[str]
        :rtype: List[int]
        """
        ns = len(s)
        nw = len(words[0])
        nws = len(words) * nw
        rs = []
        if ns < nws:
            return []
        expected = {}
        for w in words:
            expected.setdefault(w, 0)
            expected[w] += 1
        for i in xrange(ns - nws + 1):
            found = {}
            for j in xrange(len(words)):
                word = s[i + j * nw: i + (j + 1) * nw]
                if expected.get(word, 0) == 0:
                    break
                found.setdefault(word, 0)
                found[word] += 1
                if found[word] > expected[word]:
                    break
            else:
                rs.append(i)
        return rs
```
