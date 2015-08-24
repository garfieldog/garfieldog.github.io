title: Leetcode解题-Set Matrix Zeros
date: 2015-08-24 16:41:50
tags: [Leetcode, 矩阵, Array]
categories: [编程题]
---

## 描述

> Given a m x n matrix, if an element is 0, set its entire row and column to 0. Do it in place.
>
> Follow up:
> Did you use extra space?
> A straight forward solution using O(mn) space is probably a bad idea.
> A simple improvement uses O(m + n) space, but still not the best solution.
> Could you devise a constant space solution?

给一个矩阵，如果某一个单元格值为0，那么把这一整行与一整列设为0。

## 分析
这道题解出来不难，但要解得漂亮还是有一些技巧。需要多少空间复杂度呢？我们应该能轻松想到空间`O(m+n)`的算法，用`m+n`长度的哈希表记录对应行和列是否有0。事实上，我们完全可以把这个额外空间给省掉。我们有一个`m by
n`的矩阵，可以利用这个矩阵本身的存储空间来记录这个信息。就是拿出矩阵本身的一行和一列来当作我们`O(m+n)`算法中的哈希表空间。怎么取这一行和一列呢？有很多种取法。比如可以就用第一行和第一列，对他们额外处理一下就可以。或者，可以用某个0所在的行和列。需要遍历两遍数组，第一遍来记录出现0的行和列，第二遍用来对符合条件的每个位置清0。

时间复杂度`O(mn)`，空间复杂度`O(1)`。

## 代码

### Python
```python
class Solution(object):
    def setZeroes(self, A):
        """
        :type A: List[List[int]]
        :rtype: void Do not return anything, modify matrix in-place instead.
        """
        m = len(A)
        n = len(A[0])
        first_row_has0, first_col_has0 = False, False
        for i in xrange(m):
            if A[i][0] == 0:
                first_col_has0 = True
        for j in xrange(n):
            if A[0][j] == 0:
                first_row_has0 = True

        for i in xrange(1, m):
            for j in xrange(1, n):
                if A[i][j] == 0:
                    A[0][j] = 0
                    A[i][0] = 0

        for i in xrange(1, m):
            for j in xrange(1, n):
                if A[0][j] == 0 or A[i][0] == 0:
                    A[i][j] = 0

        if first_col_has0:
            for i in xrange(m):
                A[i][0] = 0
        if first_row_has0:
            for j in xrange(n):
                A[0][j] = 0
```

