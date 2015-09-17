title: Leetcode解题-Maximal Rectangle
date: 2015-09-17 10:58:14
tags: [Leetcode, 动态规划]
categories: [编程题]
---

## 描述
> Given a 2D binary matrix filled with 0's and 1's, find the largest rectangle containing all ones and return its area.

## 分析
这道题难度颇大，主题人出来我保证不打死你，双向动态规划可解，分析懒得写了，直接看[这篇文章][1]。

## 代码
### Python
```python
class Solution(object):
    def maximalRectangle(self, matrix):
        """
        :type matrix: List[List[str]]
        :rtype: int
        """
        m = len(matrix)
        if m == 0:
            return 0
        n = len(matrix[0])
        if n == 0:
            return 0
        H = [0] * n
        L = [0] * n
        R = [n] * n
        max_area = 0
        for i in xrange(m):
            left = 0
            right = n
            for j in xrange(n):
                if matrix[i][j] == '1':
                    H[j] += 1
                    L[j] = max(L[j], left)
                else:
                    left = j + 1
                    H[j] = 0
                    L[j] = 0
                    R[j] = n
            for j in xrange(n - 1, -1, -1):
                if matrix[i][j] == '1':
                    R[j] = min(R[j], right)
                    max_area = max(max_area, H[j] * (R[j] - L[j]))
                else:
                    right = j
        return max_area
```

[1]: http://liangjiabin.com/blog/2015/04/leetcode-maximal-rectangle.html
