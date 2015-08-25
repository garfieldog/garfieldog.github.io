title: Leetcode解题-Gas Station
date: 2015-08-24 18:18:32
tags: [Leetcode, Array, 贪心法]
categories: [编程题]
---

## 描述

> There are N gas stations along a circular route, where the amount of gas at station i is gas[i].
>
> You have a car with an unlimited gas tank and it costs cost[i] of gas to travel from station i to its next station (i+1). You begin the journey with an empty tank at one of the gas stations.
>
> Return the starting gas station's index if you can travel around the circuit once, otherwise return -1.
>
> Note:
> The solution is guaranteed to be unique.

## 分析
这道题等价于，对每个加油站，油的存量和到下一个加油站的消耗之差`diff[i] = gas[i] -cost[i]`这样一个循环数组，找到一个下标`x`，使得从`x`开始`diff[i]`的累加和永远非负。想到一个`O(n^2)`时间的算法很容易，但我们应该找到更好的。

首先，有一个很重要的结论，如果 $\sum\_{i=0}^{N-1} gas[i] - cost[i] >= 0 $，则肯定有解。如果小于0，则一定无解。这个结论如何证明需要仔细想一想。然后，如何找到这个下标呢？这个问题其实满足贪心法的最优子结构：

1. 从第0个加油站开始，寻找第一个使得`sum(diff[i]) < 0`的下标，如果找不到，则说明，第一个加油站就满足条件。
2. 找到这样的下标`i`，则说明`0..i`之间的加油站肯定不满足条件。可能的解只会在`i+1 ... N-1`之间。
3. 将`sum`清零，从`i+1`开始继续搜索diff累加和为负的下标`j`，找到则说明`i+1 ... j`之间的加油站都不符合条件。以此类推。
4. 最后判断全体的diff和是否非负，如果是，则按照之前的结论，肯定有解，这个解就是我们上面搜索过程中最后一个累加起始位置。

时间复杂度`O(n)`，空间复杂度`O(1)`。


## 代码

### Python
```python
class Solution(object):
    def canCompleteCircuit(self, gas, cost):
        """
        :type gas: List[int]
        :type cost: List[int]
        :rtype: int
        """
        x = 0
        n = len(gas)
        cur_sum, total_sum = 0, 0
        for i in xrange(n):
            diff = gas[i] - cost[i]
            cur_sum += diff
            total_sum += diff
            if cur_sum < 0:
                cur_sum = 0
                x = i + 1

        return x if total_sum >= 0 else -1
```

