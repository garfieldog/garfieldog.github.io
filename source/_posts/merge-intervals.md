title: Leetcode解题-Merge Intervals
date: 2015-09-18 13:49:28
tags: [Leetcode, Array]
categories: [编程题]
---

## 描述
> Given a collection of intervals, merge all overlapping intervals.
>
> For example,
> Given [1,3],[2,6],[8,10],[15,18],
> return [1,6],[8,10],[15,18].

## 分析
和[Insert Interval][1]很像，解法也很类似，先按start排序然后遍历数组前后合并。

## 代码
### Python
```python
class Solution(object):
    def merge(self, intervals):
        """
        :type intervals: List[Interval]
        :rtype: List[Interval]
        """
        if not intervals:
            return []
        intervals.sort(key=lambda x: x.start)
        rs = []
        last = intervals[0]
        for i in xrange(1, len(intervals)):
            v = intervals[i]
            if last.end < v.start:
                rs.append(last)
                last = v
            else:
                # overlap
                last.end = max(last.end, v.end)
        rs.append(last)
        return rs
```
