title: Leetcode解题-Max Points on a Line
date: 2015-09-19 11:53:09
tags: [Leetcode, Coding]
categories: [编程题]
---

## 描述
> Given n points on a 2D plane, find the maximum number of points that lie on the same straight line.

## 分析
暴力搜索的话时间`O(n^3)`，会超时。可以考虑用缓存来加速，比如对和某两点`(p1, p2)`共线的点`p3`，把`(p1, p3)`和`(p2, p3)`作为键缓存起来，下次就不用计算了。这样提交仍然超时。

考虑用斜率缓存，对于每一个点`p1`，遍历`排在它后面的点p2`(想一想为什么前面不需要)，缓存两点的斜率并缓存计数。内循环结束时更新当前最大共线数。时间`O(n^2)`。(其实用浮点存斜率有潜在的精度问题，最好是能用有理数)

## 代码
### 暴力 + 边缓存（超时且没有考虑重合点问题）
```python# Definition for a point.
class Solution(object):
    def same_line(self, p1, p2, p3):
        if p1.x == p2.x or p2.x == p3.x:
            return p1.x == p2.x == p3.x
        diff = (p3.x - p2.x) * (p2.y - p1.y) - (p3.y - p2.y) * (p2.x - p1.x)
        return diff == 0

    def maxPoints(self, points):
        """
        :type points: List[Point]
        :rtype: int
        """
        d = {}
        max_points = 0
        n = len(points)
        if n <= 2:
            return n
        for i in xrange(n - 1):
            for j in xrange(i + 1, n):
                if (points[i], points[j]) not in d:
                    candidates = []
                    for k in xrange(j + 1, n):
                        if (points[i], points[k]) not in d:
                            if self.same_line(points[i], points[j], points[k]):
                                candidates.append(points[k])
                    cur_len = len(candidates) + 2
                    d[(points[i], points[j])] = cur_len

                    for p in candidates:
                        d[(points[i], p)] = cur_len
                        d[(points[j], p)] = cur_len
                    max_points = max(max_points, cur_len)
        return max_points
```

### 斜率缓存
```python
class Solution(object):
    def slope(self, p1, p2):
        if p1.x == p2.x:
            return float('inf')
        return float(p2.y - p1.y) / (p2.x - p1.x)

    def same(self, p1, p2):
        return p1.x == p2.x and p1.y == p2.y

    def maxPoints(self, points):
        """
        :type points: List[Point]
        :rtype: int
        """
        max_points = 0
        n = len(points)
        if n <= 2:
            return n
        for i in xrange(n - 1):
            d = {}
            local_max = 1
            same_points = 0
            for j in xrange(i + 1, n):
                if self.same(points[i], points[j]):
                    same_points += 1
                    continue
                slope = self.slope(points[i], points[j])
                d.setdefault(slope, 1)
                d[slope] += 1
                local_max = max(local_max, d[slope])
            max_points = max(max_points, local_max + same_points)

        return max_points
```
