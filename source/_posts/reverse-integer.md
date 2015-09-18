title: Leetcode解题-Reverse Integer
date: 2015-09-18 10:51:22
tags: [Leetcode, Coding]
categories: [编程题]
---

## 描述
> Reverse digits of an integer.
>
> Example1: x = 123, return 321
> Example2: x = -123, return -321
>
> Have you thought about this?
> Here are some good questions to ask before coding. Bonus points for you if you have already thought through this!
>
> If the integer's last digit is 0, what should the output be? ie, cases such as 10, 100.
>
> Did you notice that the reversed integer might overflow? Assume the input is a 32-bit integer, then the reverse of 1000000003 overflows. How should you handle such cases?
>
> For the purpose of this problem, assume that your function returns 0 when the reversed integer overflows.

## 分析
算法没难度，细节实现题，测试用例里假设整数只有32位，但是Python在64位机器上int是64位的，而且一旦超出会自动转换为long，而long是没有精度限制的，所以说Python里整数不会溢出，这里为了过测试，要强行加上判断。

## 代码
### Python
```python
class Solution(object):
    def reverse(self, x):
        """
        :type x: int
        :rtype: int
        """
        sign = 1 if x >= 0 else -1
        x = abs(x)
        r = 0
        while x:
            x, mod = divmod(x, 10)
            r = r * 10 + mod
            # overflow check
            if r > 2147483647:
                return 0
        return sign * r
```
