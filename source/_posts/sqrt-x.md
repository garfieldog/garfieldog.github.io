title: Leetcode解题-Sqrt(x)
date: 2015-09-16 14:13:57
tags: [Leetcode, Math, 二分法]
categories: [编程题]
---

## 描述
> Implement int sqrt(int x).
>
> Compute and return the square root of x.

## 分析
二分查找。注意结果要向下取整时返回`high`。

## 代码
### Python
```python
class Solution(object):
    def mySqrt(self, x):
        """
        :type x: int
        :rtype: int
        """
        if x == 0:
            return 0
        if x == 1:
            return 1
        low = 1
        high = x / 2
        while low <= high:
            mid = low + (high - low) / 2
            r = mid * mid
            if r == x:
                return mid
            elif r < x:
                low = mid + 1
            else:
                high = mid - 1
        return high
```
