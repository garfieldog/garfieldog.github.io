title: Leetcode解题-String to Integer
date: 2015-08-31 17:30:39
tags: [Leetcode, String]
categories: [编程题]
---

## 描述
> Implement atoi to convert a string to an integer.
>
> Hint: Carefully consider all possible input cases. If you want a challenge, please do not see below and ask yourself what are the possible input cases.
>
> Notes: It is intended for this problem to be specified vaguely (ie, no given input specs). You are responsible to gather all the input requirements up front.

> Requirements for atoi:
> The function first discards as many whitespace characters as necessary until the first non-whitespace character is found. Then, starting from this character, takes an optional initial plus or minus sign followed by as many numerical digits as possible, and interprets them as a numerical value.
>
> The string can contain additional characters after those that form the integral number, which are ignored and have no effect on the behavior of this function.
>
> If the first sequence of non-whitespace characters in str is not a valid integral number, or if no such sequence exists because either str is empty or it contains only whitespace characters, no conversion is performed.
>
> If no valid conversion could be performed, a zero value is returned. If the correct value is out of the range of representable values, INT\_MAX (2147483647) or INT\_MIN (-2147483648) is returned.

## 分析
简单题，但要想全各种输入情况。

## 代码

### Python
```python
class Solution(object):
    def myAtoi(self, str):
        """
        :type str: str
        :rtype: int
        """
        n = len(str)
        # skip leading-whitespaces
        i = 0
        while i < n and str[i] == ' ':
            i += 1
        if i >= n:
            return 0

        sign = 1
        if str[i] == '+':
            sign = 1
            i += 1
        elif str[i] == '-':
            sign = -1
            i += 1

        x = 0
        int_max, int_min = 2147483647, -2147483648
        while i < n and str[i].isdigit():
            x = x * 10 + int(str[i])
            i += 1

        x *= sign
        x = min(int_max, x)
        x = max(int_min, x)
        return x
```
