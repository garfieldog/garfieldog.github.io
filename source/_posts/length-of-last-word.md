title: Leetcode解题-Length of Last Word
date: 2015-09-06 17:42:05
tags: [Leetcode, String]
categories: [编程题]
---

## 描述
> Given a string s consists of upper/lower-case alphabets and empty space characters ' ', return the length of last word in the string.
>
> If the last word does not exist, return 0.
>
> Note: A word is defined as a character sequence consists of non-space characters only.
>
> For example, 
> Given s = "Hello World",
> return 5.

## 分析
简单题，时间`O(n)`, 空间`O(1)`。

## 代码
### One Line Solver
```python
class Solution(object):
    def lengthOfLastWord(self, s):
        """
        :type s: str
        :rtype: int
        """
        return len(s.rstrip().split(' ')[-1])
```

### 迭代
```python
class Solution(object):
    def lengthOfLastWord(self, s):
        """
        :type s: str
        :rtype: int
        """
        n = 0
        last_space = True
        for c in s:
            if c == ' ':
                last_space = True
                continue

            n = 1 if last_space else n + 1
            last_space = False
        return n
```
