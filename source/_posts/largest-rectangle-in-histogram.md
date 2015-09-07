title: Leetcode解题-Largest Rectangle in Histogram
date: 2015-09-07 13:15:40
tags: [Leetcode, Stack]
categories: [编程题]
---

## 描述
> Given n non-negative integers representing the histogram's bar height where the width of each bar is 1, find the area of largest rectangle in the histogram.
>
> ![histogram](/images/histogram.png)
> Above is a histogram where width of each bar is 1, given height = [2,1,5,6,2,3].
>
> ![histogram-area](/images/histogram_area.png)
> The largest rectangle is shown in the shaded area, which has area = 10 unit.
>
> For example,
> Given height = [2,1,5,6,2,3],
> return 10.

## 分析
时间`O(n^2)`的算法很容易想，每个位置上向两边扩散就可以。不过还可以更好：利用一个栈，栈内维护递增的序列，遇到破坏递增的元素就持续出栈（这时栈顶元素能围成多大的矩形已经可以计算），直到当前元素大于栈顶，继续入栈。详细分析可参考[这篇文章][1]。

注意`if not ss or height[i] > height[ss[-1]]:` 中的判断`>`还是`>=`不影响正确性，想想为什么。

## 代码
### Python
```python
class Solution(object):
    def largestRectangleArea(self, height):
        """
        :type height: List[int]
        :rtype: int
        """
        ss = []
        max_area = 0
        height.append(0)
        n = len(height)
        i = 0
        while i < n:
            if not ss or height[i] > height[ss[-1]]:
                ss.append(i)
                i += 1
            else:
                idx = ss.pop()
                w = i if not ss else i - 1 - ss[-1]
                max_area = max(max_area, height[idx] * w)
        return max_area
```

[1]: http://www.cnblogs.com/lichen782/p/leetcode_Largest_Rectangle_in_Histogram.html
