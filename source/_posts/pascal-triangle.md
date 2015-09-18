title: Leetcode解题-Pascal Triangle
date: 2015-09-18 17:06:31
tags: [Leetcode, Array, Coding]
categories: [编程题]
---

## 描述
> Given numRows, generate the first numRows of Pascal's triangle.
>
> For example, given numRows = 5,
> Return
>
> [
>      [1],
>     [1,1],
>    [1,2,1],
>   [1,3,3,1],
>  [1,4,6,4,1]
> ]

## 分析
比较简单，打印杨辉三角。

## 代码
### Python
```python
class Solution(object):
    def generate(self, numRows):
        """
        :type numRows: int
        :rtype: List[List[int]]
        """
        if numRows == 0:
            return []
        rs = [[1]]
        for i in xrange(1, numRows):
            row = [1]
            for j in xrange(1, i):
                row.append(rs[i - 1][j - 1] + rs[i - 1][j])
            row.append(1)
            rs.append(row)
        return rs
```
