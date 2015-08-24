title: Leetcode解题-Climbing Stairs
date: 2015-08-24 14:14:27
tags: [Leetcode, Fibonacci, 动态规划]
categories: [编程题]
---

## 描述

> You are climbing a stair case. It takes n steps to reach to the top.
>
> Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

## 分析

稍一分析就知道答案是斐波那契数`F(n + 1)`。因为`f(1) = 1, f(2) = 2`，而`n > 2`时，有多少种走法呢，可以分解为：

1. 如果第一次走一步，那么有`f(n-1)`种走法。
2. 如果第一次走两步，那么有`f(n-2)`种走法。
3. 因此`f(n) = f(n-1) + f(n-2)`，故`f(n)`是第`n+1`个斐波那契数。

使用动态规划算法，时间复杂度`O(n)`，空间复杂度`O(1)`。

## 代码

### Python
```python
class Solution(object):
    def climbStairs(self, n):
        """
        :type n: int
        :rtype: int
        """
        if n <= 2:
            return n
        a, b = 1, 2
        for i in xrange(n - 2):
            a, b = b, a + b
        return b
```


