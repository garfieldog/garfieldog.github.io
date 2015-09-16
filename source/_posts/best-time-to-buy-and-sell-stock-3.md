title: Leetcode解题-Best Time to Buy and Sell Stock III
date: 2015-09-16 16:17:46
tags: [Leetcode, Array, 动态规划]
categories: [编程题]
---

## 描述
> Say you have an array for which the ith element is the price of a given stock on day i.
>
> Design an algorithm to find the maximum profit. You may complete at most two transactions.
>
> Note:
> You may not engage in multiple transactions at the same time (ie, you must sell the stock before you buy again).

## 分析
[Best Time to Buy and Sell Stock][1]的后继问题，这次可以买卖两次，但任何时刻手上最多只能持有1股。这下就难了不少，可以考虑分治法，遍历数组位置`i`，分别用[这一题][1]中的算法求`[0..i]`和`[i..n-1]`的最大利润，再挑选最佳位置`i`。时间复杂度`O(n^2)`，这个解法会超时。

我们观察上面这个算法，它要求的`f(0, i), 0 <= i < n`其实可以在一次遍历中全部求出，只要我们的算法加一个缓存数组就可以了。同理`f(i, n)`也是一样的，倒着求就行。这样一来，我们只要扫描两遍数组，就能得到想要的部分解了。时间复杂度降到了`O(n)`，空间`O(n)`。有点像[Trapping Rain Water][3]的解法。

## 代码
### 分治法（超时）
```python
class Solution(object):
    def maxProfitPartial(self, prices, start, end):
        n = end - start + 1
        if n <= 1:
            return 0
        profit = 0
        cur_min = prices[start]
        for i in xrange(start + 1, end + 1):
            profit = max(profit, prices[i] - cur_min)
            cur_min = min(cur_min, prices[i])
        return profit

    def maxProfit(self, prices):
        """
        :type prices: List[int]
        :rtype: int
        """
        max_profit = 0
        n = len(prices)
        if n <= 1:
            return 0
        for i in xrange(n):
            profit = self.maxProfitPartial(prices, 0, i) + self.maxProfitPartial(prices, i, n - 1)
            max_profit = max(max_profit, profit)
        return max_profit
```

### 动态规划
```python
class Solution(object):
    def maxProfitPartial(self, prices, start, end):
        n = end - start + 1
        if n <= 1:
            return 0
        profit = 0
        cur_min = prices[start]
        for i in xrange(start + 1, end + 1):
            profit = max(profit, prices[i] - cur_min)
            cur_min = min(cur_min, prices[i])
        return profit

    def maxProfit(self, prices):
        """
        :type prices: List[int]
        :rtype: int
        """
        n = len(prices)
        if n <= 1:
            return 0
        left = [0] * n
        cur_min = prices[0]
        for i in xrange(1, n):
            left[i] = max(left[i - 1], prices[i] - cur_min)
            cur_min = min(cur_min, prices[i])

        profit = 0
        max_profit = 0
        cur_max = prices[n - 1]
        for i in xrange(n - 1, -1, -1):
            profit = max(profit, cur_max - prices[i])
            cur_max = max(cur_max, prices[i])
            max_profit = max(max_profit, profit + left[i])

        return max_profit
```

[1]: /2015/09/16/best-time-to-buy-and-sell-stock/
[2]: /2015/09/16/best-time-to-buy-and-sell-stock-2/
[3]: /2015/08/22/trapping-rain-water/
