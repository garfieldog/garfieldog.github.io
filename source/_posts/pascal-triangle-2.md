title: Leetcode解题-Pascal Triangle II
date: 2015-09-18 17:18:14
tags: [Leetcode, Array, Coding]
categories: [编程题]
---

## 描述
> Given an index k, return the kth row of the Pascal's triangle.
>
> For example, given k = 3,
> Return [1,3,3,1].

## 分析
[Pascal Triangle][1]的后续。用类似动态规划的降维方式，可以实现空间`O(n)`的算法。

## 代码
### Python
```python
class Solution(object):
    def getRow(self, rowIndex):
        """
        :type rowIndex: int
        :rtype: List[int]
        """
        rs = [0] * (rowIndex + 1)
        rs[0] = 1
        for i in xrange(1, rowIndex + 1):
            rs[i] = 1
            for j in xrange(i - 1, 0, -1):
                rs[j] += rs[j - 1]
        return rs
```

[1]: /2015/09/18/pascal-triangle/
