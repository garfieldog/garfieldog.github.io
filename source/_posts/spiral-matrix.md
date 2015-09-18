title: Leetcode解题-Spiral Matrix
date: 2015-09-18 17:33:21
tags: [Leetcode, Matrix, Coding]
categories: [编程题]
---

## 描述
> Given a matrix of m x n elements (m rows, n columns), return all elements of the matrix in spiral order.
>
> For example,
> Given the following matrix:
>
> [
>  [ 1, 2, 3 ],
>  [ 4, 5, 6 ],
>  [ 7, 8, 9 ]
> ]
> You should return [1,2,3,6,9,8,7,4,5].

## 分析
细节实现题，注意边界判断。

## 代码
### Python
```python
class Solution(object):
    def spiralOrder(self, matrix):
        """
        :type matrix: List[List[int]]
        :rtype: List[int]
        """
        if not matrix:
            return []
        up = 0
        down = len(matrix) - 1
        left = 0
        right = len(matrix[0]) - 1
        rs = []
        while right >= left and down >= up:
            if right >= left and down >= up:
                for i in xrange(left, right + 1):
                    rs.append(matrix[up][i])
                up += 1
            if down >= up and right >= left:
                for i in xrange(up, down + 1):
                    rs.append(matrix[i][right])
                right -= 1
            if right >= left and down >= up:
                for i in xrange(right, left - 1, -1):
                    rs.append(matrix[down][i])
                down -= 1
            if down >= up and right >= left:
                for i in xrange(down, up - 1, -1):
                    rs.append(matrix[i][left])
                left += 1
        return rs
```
