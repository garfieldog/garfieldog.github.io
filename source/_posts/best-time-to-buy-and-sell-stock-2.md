title: Leetcode解题-Best Time to Buy and Sell Stock II
date: 2015-09-16 16:04:56
tags: [Leetcode, Array]
categories: [编程题]
---

## 描述
> Say you have an array for which the ith element is the price of a given stock on day i.
>
> Design an algorithm to find the maximum profit. You may complete as many transactions as you like (ie, buy one and sell one share of the stock multiple times). However, you may not engage in multiple transactions at the same time (ie, you must sell the stock before you buy again).

## 分析
[上一题][1]的后继问题，这次仍然做时候诸葛亮，而且可以买卖多次，但是有个条件就是手上最多持有1股。非常简单，就是找每一个递增的区间，在区间底部买入，顶部卖出即可，一遍扫描。

## 代码
### Python
```python
class Solution(object):
    def maxProfit(self, prices):
        """
        :type prices: List[int]
        :rtype: int
        """
        n = len(prices)
        profit = 0
        for i in xrange(1, n):
            diff = prices[i] - prices[i - 1]
            profit += max(0, diff)
        return profit
```

[1]: /2015/09/16/best-time-to-buy-and-sell-stock/
