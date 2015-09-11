title: Leetcode解题-Search a 2D Matrix
date: 2015-09-11 15:29:34
tags: [Leetcode, Array, 二分法]
categories: [编程题]
---

## 描述
> Write an efficient algorithm that searches for a value in an m x n matrix. This matrix has the following properties:
>
> Integers in each row are sorted from left to right.
> The first integer of each row is greater than the last integer of the previous row.
> For example,
>
> Consider the following matrix:
>
> [
>   [1,   3,  5,  7],
>   [10, 11, 16, 20],
>   [23, 30, 34, 50]
> ]
> Given target = 3, return true.

## 分析
就是二分查找，多一个坐标转换。

## 代码
### Python
```python
class Solution(object):
    def searchMatrix(self, matrix, target):
        """
        :type matrix: List[List[int]]
        :type target: int
        :rtype: bool
        """
        m = len(matrix)
        if m == 0:
            return False
        n = len(matrix[0])
        low = 0
        high = m * n - 1
        while low <= high:
            mid = low + (high - low) / 2
            x, y = divmod(mid, n)
            if matrix[x][y] == target:
                return True
            elif matrix[x][y] > target:
                high = mid - 1
            else:
                low = mid + 1
        return False
```
