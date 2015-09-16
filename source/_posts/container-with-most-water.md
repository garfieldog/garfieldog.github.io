title: Leetcode解题-Container with Most Water
date: 2015-09-16 18:36:15
tags: [Leetcode, Array, 贪心法, 两指针]
categories: [编程题]
---

## 描述
> Given n non-negative integers a1, a2, ..., an, where each represents a point at coordinate (i, ai). n vertical lines are drawn such that the two endpoints of line i is at (i, ai) and (i, 0). Find two lines, which together with x-axis forms a container, such that the container contains the most water.
>
> Note: You may not slant the container.

## 分析
`O(n^2)`的算法很简单，双重循环找到最优解，但显然超时。可以只用一次遍历，使用两指针，分别从头和从尾部开始，计算他们之间的面积，如果头部的木板比尾部的低，则可以直接将头指针后移，因为这已经是以它为第一块木板所能够围成的最大面积。如果比尾部高，则尾指针前移。很像[Trapping Rain Water][1]。

## 代码
### Python
```python
class Solution(object):
    def maxArea(self, height):
        """
        :type height: List[int]
        :rtype: int
        """
        max_area = 0
        low = 0
        high = len(height) - 1
        while (low < high):
            area = min(height[low], height[high]) * (high - low)
            max_area = max(max_area, area)
            if height[low] <= height[high]:
                low += 1
            else:
                high -= 1
        return max_area
```

[1]: /2015/08/22/trapping-rain-water/
