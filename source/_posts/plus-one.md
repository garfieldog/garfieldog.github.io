title: Leetcode解题-Plus One
date: 2015-08-24 13:57:51
tags: [Leetcode, Array]
categories: [编程题]
---

## 描述

> Given a non-negative number represented as an array of digits, plus one to the number.
>
> The digits are stored such that the most significant digit is at the head of the list.

## 分析

没什么好分析的，循环进位。

## 代码

### Python
```python
class Solution(object):
    def plusOne(self, digits):
        """
        :type digits: List[int]
        :rtype: List[int]
        """
        carry = 1
        for i in xrange(len(digits) - 1, -1, -1):
            s = digits[i] + carry
            carry, r = divmod(s, 10)
            digits[i] = r
        if carry > 0:
            digits.insert(0, 1)
        return digits
```
