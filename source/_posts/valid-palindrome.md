title: Leetcode解题-Valid Palindrome
date: 2015-08-31 11:36:02
tags: [Leetcode, String, 两指针]
categories: [编程题]
---

## 描述
> Given a string, determine if it is a palindrome, considering only alphanumeric characters and ignoring cases.
>
> For example,
> "A man, a plan, a canal: Panama" is a palindrome.
> "race a car" is not a palindrome.
>
> Note:
> Have you consider that the string might be empty? This is a good question to ask during an interview.
>
> For the purpose of this problem, we define empty string as valid palindrome.

## 分析
简单题，判断是否回文。用两指针，分别从头和尾相向而行，时间`O(n)`，空间`O(1)`。

## 代码

###Python
```python
class Solution(object):
    def isPalindrome(self, s):
        """
        :type s: str
        :rtype: bool
        """
        i, j = 0, len(s) - 1
        while i < j:
            if not s[i].isalnum():
                i += 1
            elif not s[j].isalnum():
                j -= 1
            elif s[i].lower() == s[j].lower():
                i += 1
                j -= 1
            else:
                return False
        return True
```
