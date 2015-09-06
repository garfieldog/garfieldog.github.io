title: Leetcode解题-Roman to Integer
date: 2015-09-06 15:45:37
tags: [Leetcode, String]
categories: [编程题]
---

## 描述
> Given a roman numeral, convert it to an integer.
>
> Input is guaranteed to be within the range from 1 to 3999

## 分析
比[Integer to Roman][1]简单多了，是加法规则还是减法规则很好判断。

## 代码
### Python
```python
class Solution(object):
    def romanToInt(self, s):
        """
        :type s: str
        :rtype: int
        """

        d = {
            'M': 1000,
            'D': 500,
            'C': 100,
            'L': 50,
            'X': 10,
            'V': 5,
            'I': 1
        }

        n = len(s)
        r = 0
        for i in xrange(n):
            a = d[s[i]]
            if i < n - 1 and a < d[s[i + 1]]:
                a = -a
            r += a
        return r
```

[1]: /2015/09/06/integer-to-roman/
