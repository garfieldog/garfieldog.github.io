title: Leetcode解题-Best Time to Buy and Sell Stock
date: 2015-09-16 15:50:49
tags: [Leetcode, Array, 贪心法]
categories: [编程题]
---

## 描述
> Say you have an array for which the ith element is the price of a given stock on day i.
>
> If you were only permitted to complete at most one transaction (ie, buy one and sell one share of the stock), design an algorithm to find the maximum profit.

## 分析
要理解题意，给定一只股票一段时间内每天的估价，做一下事后诸葛亮，问如果只做一次交易（买一次买一次，注意不能卖空，所以必须先买后卖），所以就是找到低价，然后高价卖出，要求是低价必须在高价前面。扫描一遍数组即可，维护当前的最大利润和当前最低价。

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
        if n <= 1:
            return 0
        profit = 0
        cur_min = prices[0]
        for i in xrange(1, n):
            profit = max(profit, prices[i] - cur_min)
            cur_min = min(cur_min, prices[i])
        return profit
```
