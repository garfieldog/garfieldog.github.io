title: Leetcode解题-Longest Valid Parentheses
date: 2015-09-06 19:33:29
tags: [Leetcode, Stack]
categories: [编程题]
---

## 描述
> Given a string containing just the characters '(' and ')', find the length of the longest valid (well-formed) parentheses substring.
>
> For "(()", the longest valid parentheses substring is "()", which has length = 2.
>
> Another example is ")()())", where the longest valid parentheses substring is "()()", which has length = 4.
## 分析
稍有难度，使用栈，时间`O(n)`，空间`O(n)`。

## 代码
### Python
```python
class Solution(object):
    def longestValidParentheses(self, s):
        """
        :type s: str
        :rtype: int
        """
        ss = []
        n = len(s)
        max_len = 0
        last = -1
        for i in xrange(n):
            if s[i] == '(':
                ss.append(i)
                continue

            if not ss:
                last = i
            else:
                ss.pop()
                if not ss:
                    max_len = max(max_len, i - last)
                else:
                    max_len = max(max_len, i - ss[-1])
        return max_len
```
