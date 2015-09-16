title: Leetcode解题-Longest Substring Without Repeating Characters
date: 2015-09-16 17:53:57
tags: [Leetcode, String, 贪心法]
categories: [编程题]
---

## 描述
> Given a string, find the length of the longest substring without repeating characters. For example, the longest substring without repeating letters for "abcabcbb" is "abc", which the length is 3. For "bbbbb" the longest substring is "b", with the length of 1.

## 分析
`O(n^2)`的算法很容易想，在每个位置上找满足要求的子串。必然会超时。我们借用KMP类似的思想，发现重复字符时步子可以迈得大一点。我们发现在重复字符上一次出现之前的部分都不用在搜索了，因为肯定不会产生比现有子串更长的了。

## 代码
### Python
```python
class Solution(object):
    def lengthOfLongestSubstring(self, s):
        """
        :type s: str
        :rtype: int
        """
        last = {}
        start = 0
        max_len = 0
        n = len(s)
        for i in xrange(n):
            last_idx = last.get(s[i], -1)
            if last_idx >= start:
                max_len = max(i - start, max_len)
                start = last_idx + 1
            last[s[i]] = i
        return max(n - start, max_len)
```
