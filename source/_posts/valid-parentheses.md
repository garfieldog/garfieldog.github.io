title: Leetcode解题-Valid Parentheses
date: 2015-09-06 19:23:59
tags: [Leetcode, Stack]
categories: [编程题]
---

## 描述
> Given a string containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.
>
> The brackets must close in the correct order, "()" and "()[]{}" are all valid but "(]" and "([)]" are not.

## 分析
简单的Stack题，时间`O(n)`，空间`O(1)`。

## 代码
### Python
```python
class Solution(object):
    def isValid(self, s):
        """
        :type s: str
        :rtype: bool
        """
        d = {
            ')': '(',
            '}': '{',
            ']': '['
        }
        ss = []
        for c in s:
            if c in '({[':
                ss.append(c)
            elif c in ')}]':
                if not ss or d[c] != ss[-1]:
                    return False
                ss.pop()
        return not ss
```
