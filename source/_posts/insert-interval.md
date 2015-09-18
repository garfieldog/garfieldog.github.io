title: Leetcode解题-Insert Interval
date: 2015-09-18 11:33:32
tags: [Leetcode, Array]
categories: [编程题]
---

## 描述
> Given a set of non-overlapping intervals, insert a new interval into the intervals (merge if necessary).
>
> You may assume that the intervals were initially sorted according to their start times.
>
> Example 1:
> Given intervals [1,3],[6,9], insert and merge [2,5] in as [1,5],[6,9].
>
> Example 2:
> Given [1,2],[3,5],[6,7],[8,10],[12,16], insert and merge [4,9] in as [1,2],[3,10],[12,16].
>
> This is because the new interval [4,9] overlaps with [3,5],[6,7],[8,10].

## 分析
看似简单，写对了不容易。思路是这样的，遍历已有区间，和新区间进行比较，有三种情况

1. 没有重叠，当前区间整体在新区间前面，则当前区间添加到结果集。
2. 没有重叠，当前区间整体在新区间后面，添加新区间到结果集。后面的区间可以一一添加即可。
3. 有重叠，把当前区间和新区间合并，生成的新区间继续和后面的区间进行上述过程。

## 代码
### Python
```python
class Solution(object):
    def insert(self, intervals, newInterval):
        """
        :type intervals: List[Interval]
        :type newInterval: Interval
        :rtype: List[Interval]
        """
        rs = []
        for v in intervals:
            if v.end < newInterval.start:
                rs.append(v)
            elif v.start > newInterval.end:
                rs.append(newInterval)
                newInterval = v
            else:
                # overlap
                newInterval.start = min(v.start, newInterval.start)
                newInterval.end = max(v.end, newInterval.end)
        rs.append(newInterval)
        return rs
```
