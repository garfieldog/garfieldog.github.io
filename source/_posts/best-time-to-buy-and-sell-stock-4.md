title: Leetcode解题-Best Time to Buy and Sell Stock IV
date: 2015-09-16 17:06:38
tags: [Leetcode, Array, 动态规划]
categories: [编程题]
---

## 描述
> Say you have an array for which the ith element is the price of a given stock on day i.
>
> Design an algorithm to find the maximum profit. You may complete at most k transactions.
>
> Note:
> You may not engage in multiple transactions at the same time (ie, you must sell the stock before you buy again).

## 分析
[Best Time to Buy and Sell Stock][1]的后继问题，这次彻底灵活了，可以买卖k次，同样任何时刻手上最多持有1股。

如果`k > n / 2` 其实就退化成了不限次数买卖的情况，就是[系列中的第二题][2]的情况。然后我们构造这样一个二维动态规划状态转移方程，令`local[i][j]`为在截止第i天最多可j次交易并且最后一次交易在最后一天卖出的最大利润，`global[i][j]`为在截止第i天时最多可j次交易的最大利润，目标就是`global[n - 1][k]`。

    local[i][j] = max(global[i - 1][j - 1] + max(diff, 0), local[i - 1][j] + diff)
    global[i][j] = max(local[i][j], global[i - 1][j])


## 代码
### Python
```python
class Solution(object):
    def maxProfit(self, k, prices):
        """
        :type k: int
        :type prices: List[int]
        :rtype: int
        """
        n = len(prices)
        if n <= 1:
            return 0
        if k > n / 2:
            return self.maxProfitNoLimit(prices)
        l = [0] * (k + 1)
        g = [0] * (k + 1)
        for i in xrange(1, n):
            diff = prices[i] - prices[i - 1]
            for j in xrange(k, 0, -1):
                l[j] = max(g[j - 1] + max(diff, 0), l[j] + diff)
                g[j] = max(l[j], g[j])
        return g[k]

    def maxProfitNoLimit(self, prices):
        n = len(prices)
        profit = 0
        for i in xrange(1, n):
            diff = prices[i] - prices[i - 1]
            profit += max(0, diff)
        return profit
```

[1]: /2015/09/16/best-time-to-buy-and-sell-stock/
[2]: /2015/09/16/best-time-to-buy-and-sell-stock-2/
