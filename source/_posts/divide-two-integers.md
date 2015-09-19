title: Leetcode解题-Divide Two Integers
date: 2015-09-19 10:38:05
tags: [Leetcode, Coding]
categories: [编程题]
---

## 描述
> Divide two integers without using multiplication, division and mod operator.
>
> If it is overflow, return MAX\_INT.

## 分析
不用乘法、除法、取模运算来实现除法。可以只用加减法来实现，但是太慢了。可以用位运算来加速。

## 代码
### Python
```python
class Solution(object):
    def divide(self, dividend, divisor):
        """
        :type dividend: int
        :type divisor: int
        :rtype: int
        """
        MAX_INT = (1 << 31) - 1
        r = 0
        p1 = dividend > 0
        p2 = divisor > 0
        sign = -1 if p1 ^ p2 else 1
        dividend = abs(dividend)
        divisor = abs(divisor)
        while dividend >= divisor:
            d = divisor
            i = 1
            while d <= dividend:
                dividend -= d
                r += i
                d <<= 1
                i <<= 1
        return min(sign * r, MAX_INT)
```
