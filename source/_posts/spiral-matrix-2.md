title: Leetcode解题-Spiral Matrix II
date: 2015-09-18 18:04:01
tags: [Leetcode, Matrix, Coding]
categories: [编程题]
---

## 描述
> Given an integer n, generate a square matrix filled with elements from 1 to n2 in spiral order.
>
> For example,
> Given n = 3,
>
> You should return the following matrix:
> [
>  [ 1, 2, 3 ],
>  [ 8, 9, 4 ],
>  [ 7, 6, 5 ]
> ]

## 分析
[Spiral Matrix][1]的后续。解法是一样的。

## 代码
### Python
```python
class Solution(object):
    def generateMatrix(self, n):
        """
        :type n: int
        :rtype: List[List[int]]
        """
        if n == 0:
            return []
        rs = [[0] * n for i in xrange(n)]
        left = up = 0
        right = down = n - 1
        x = 1
        while right >= left and down >= up:
            if right >= left and down >= up:
                for i in xrange(left, right + 1):
                    rs[up][i] = x
                    x += 1
                up += 1
            if down >= up and right >= left:
                for i in xrange(up, down + 1):
                    rs[i][right] = x
                    x += 1
                right -= 1
            if right >= left and down >= up:
                for i in xrange(right, left - 1, -1):
                    rs[down][i] = x
                    x += 1
                down -= 1
            if down >= up and right >= left:
                for i in xrange(down, up - 1, -1):
                    rs[i][left] = x
                    x += 1
                left += 1
        return rs
```

[1]: /2015/09/18/spiral-matrix/
