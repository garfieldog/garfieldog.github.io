title: Leetcode解题-Pow(x, n)
date: 2015-09-16 13:47:11
tags: [Leetcode, Math, 二分法]
categories: [编程题]
---

## 描述
> Implement pow(x, n).

## 分析
二分法，递归很简单，迭代有一定技巧。

## 代码
### 递归
```python
class Solution(object):
    def myPow(self, x, n):
        """
        :type x: float
        :type n: int
        :rtype: float
        """
        if n == 0:
            return 1.0
        positive = n > 0
        n = abs(n)
        if n % 2 == 1:
            r = x * self.myPow(x, n - 1)
        else:
            r = self.myPow(x, n / 2)
            r = r * r
        return r if positive else 1 / r
```

### 迭代
```python
class Solution(object):
    def myPow(self, x, n):
        """
        :type x: float
        :type n: int
        :rtype: float
        """
        if n == 0:
            return 1.0
        if n < 0:
            return 1.0 / self.myPow(x, -n)
        left = x
        right = 1.0
        while n > 1:
            if n % 2 == 1:
                right *= left
            left *= left
            n /= 2
        return left * right
```
