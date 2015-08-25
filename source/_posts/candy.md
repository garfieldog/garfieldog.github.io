title: Leetcode解题-Candy
date: 2015-08-25 10:36:28
tags: [Leetcode, Array, 动态规划]
categories: [编程题]
---

## 描述

> There are N children standing in a line. Each child is assigned a rating value.
>
> You are giving candies to these children subjected to the following requirements:
>
> Each child must have at least one candy.
> Children with a higher rating get more candies than their neighbors.
> What is the minimum candies you must give?

## 分析
有一定难度。对于某个位置`i`上的小孩，它的糖果数取决于他自己和左右邻居的关系。设`ratings`数组为`R`，分配给小孩的糖果数为数组`C`。我们可以这样来考虑这个问题，拆分为两个步骤：

1. 首先，如果只要求`C[i] > C[i-1]` iff `R[i] > R[i-1]`，也就是说只考虑每个小孩左手边的小孩，那么如果`R[i] > R[i-1]`则`C[i] = C[i-1] + 1`，否则`C[i] = 1`。
2. 然后我们再考虑加上右手边小孩的限制，如果`R[i] > R[i+1]`，则`C[i] = max(C[i+1] + 1, C[i])`。

这样一来，考虑到上面被分解的两个问题内部的互相依赖情况，我们就可以用两个循环分别从左到右、从右到左遍历数组，得到时间`O(n)`，空间`O(1)`的算法。

## 代码

### Python
```python
class Solution(object):
    def candy(self, R):
        """
        :type R: List[int]
        :rtype: int
        """
        n = len(R)
        C = [1] * n
        for i in xrange(1, n):
            if R[i] > R[i - 1]:
                C[i] = C[i - 1] + 1

        for i in xrange(n - 2, -1, -1):
            if R[i] > R[i + 1]:
                C[i] = max(C[i + 1] + 1, C[i])

        return sum(C)
```
