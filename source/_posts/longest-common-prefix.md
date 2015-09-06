title: Leetcode解题-Longest Common Prefix
date: 2015-09-06 09:43:36
tags: [Leetcode, String]
categories: [编程题]
---

## 描述
> Write a function to find the longest common prefix string amongst an array of strings.

## 分析
简单题，但容易想复杂。第一反应是用trie树，可以做，但实现较复杂。其实只要按位置依次比对每一个字符串，直到有不相等的情况出现即可。时间复杂度`O(n1 + n2 + ...)`，空间复杂度`O(1)`。

## 代码
### Python
```python
class Solution(object):
    def longestCommonPrefix(self, strs):
        """
        :type strs: List[str]
        :rtype: str
        """
        if not strs:
            return ''
        idx = 0
        for i in xrange(len(strs[0])):
            stop = False
            for j in xrange(1, len(strs)):
                if len(strs[j]) <= i or strs[0][i] != strs[j][i]:
                    stop = True
                    break
            if stop:
                break
            idx += 1
        return strs[0][:idx]
```

