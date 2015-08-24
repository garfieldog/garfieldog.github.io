title: Leetcode解题-Rotate Image
date: 2015-08-24 15:41:53
tags: [Leetcode, 矩阵, 数学]
categories: [编程题]
---

## 描述

> You are given an n x n 2D matrix representing an image.
>
> Rotate the image by 90 degrees (clockwise).
>
> Follow up:
> Could you do this in-place?

## 分析
将矩阵顺时针旋转90°，等同于先沿水平中线翻转，再按主对角线翻转。


## 代码

### Python
```python
class Solution(object):
    def rotate(self, matrix):
        """
        :type matrix: List[List[int]]
        :rtype: void Do not return anything, modify matrix in-place instead.
        """
        n = len(matrix)
        for i in xrange(n / 2):
            for j in xrange(n):
                matrix[i][j], matrix[n - 1 - i][j] = matrix[n - 1 - i][j], matrix[i][j]

        for i in xrange(n):
            for j in xrange(i):
                matrix[i][j], matrix[j][i] = matrix[j][i], matrix[i][j]
```
