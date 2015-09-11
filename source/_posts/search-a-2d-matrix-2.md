title: Leetcode解题-Search a 2D Matrix II
date: 2015-09-11 15:56:13
tags: [Leetcode, Array, 二分法]
categories: [编程题]
---

## 描述
> Write an efficient algorithm that searches for a value in an m x n matrix. This matrix has the following properties:
>
> Integers in each row are sorted in ascending from left to right.
> Integers in each column are sorted in ascending from top to bottom.
> For example,
>
> Consider the following matrix:
>
> [
>   [1,   4,  7, 11, 15],
>   [2,   5,  8, 12, 19],
>   [3,   6,  9, 16, 22],
>   [10, 13, 14, 17, 24],
>   [18, 21, 23, 26, 30]
> ]
> Given target = 5, return true.
>
> Given target = 20, return false.

## 分析
[上一题][1]的升级版。这次矩阵每一行是排序的，每一列也是排序的，但不保证前一行的所有数小于后一行的。仍然使用二分查找，不过每次只能剔除`1/4`的元素。(如果中心值比目标大，则剔除右下角的矩阵块，如果小，则剔除左上角)

## 代码
### Python
```python
class Solution(object):
    def searchMatrixR(self, matrix, x1, y1, x2, y2, target):
        if x1 > x2 or y1 > y2:
            return False
        mid_x = x1 + (x2 - x1) / 2
        mid_y = y1 + (y2 - y1) / 2
        if matrix[mid_x][mid_y] == target:
            return True
        elif matrix[mid_x][mid_y] > target:
            return self.searchMatrixR(matrix, x1, y1, mid_x - 1, y2, target) or \
                self.searchMatrixR(matrix, mid_x, y1, x2, mid_y - 1, target)
        else:
            return self.searchMatrixR(matrix, x1, mid_y + 1, mid_x, y2, target) or \
                self.searchMatrixR(matrix, mid_x + 1, y1, x2, y2, target)

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
        return self.searchMatrixR(matrix, 0, 0, m - 1, n - 1, target)
```

[1]: /2015/09/11/search-a-2d-matrix/
