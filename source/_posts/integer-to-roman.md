title: Leetcode解题-Integer to Roman
date: 2015-09-06 14:06:29
tags: [Leetcode, String]
categories: [编程题]
---

## 描述
> Given an integer, convert it to a roman numeral.
>
> Input is guaranteed to be within the range from 1 to 3999.

## 分析
要考虑[罗马数字][1]的加法规则和减法规则，要写对还是有一定技巧的，下面是一个精巧的解法。

## 代码
### Python
```python
class Solution(object):
    def intToRoman(self, num):
        """
        :type num: int
        :rtype: str
        """
        romans = [
            ('M', 1000),
            ('CM', 900),
            ('D', 500),
            ('CD', 400),
            ('C', 100),
            ('XC', 90),
            ('L', 50),
            ('XL', 40),
            ('X', 10),
            ('IX', 9),
            ('V', 5),
            ('IV', 4),
            ('I', 1)
        ]
        rs = []
        for s, n in romans:
            c, num = divmod(num, n)
            rs.extend([s] * c)
        return ''.join(rs)
```

[1]: https://zh.wikipedia.org/wiki/%E7%BD%97%E9%A9%AC%E6%95%B0%E5%AD%97
