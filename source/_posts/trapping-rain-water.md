title: Leetcode解题-Trapping Rain Water
date: 2015-08-22 18:06:40
tags: [Leetcode, Array, 两指针]
categories: [编程题]
---

## 描述

> Given n non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it is able to trap after raining.
>
> For example, 
> Given [0,1,0,2,1,0,1,3,2,1,2,1], return 6.
>
> ![trapping-rain-water](/images/rainwatertrap.png) 

这道题非常经典。给一排高低不等的木板，求下雨后能存多少水。

## 分析

对于某一块木板而言，它能存多少水取决于它左边最高的板与右边最高的板中较小的那个：`min(max_left, max_right) -
height`。可以遍历两遍数组，一次从左到右，记录每块板左边最高板的高度，第二次从右到左，记录每块板右边最高板的高度。时间与空间复杂度都是`O(n)`。

还可以再极端一点，只遍历一次数组，使用两指针前后遍历，比较两指针当前的值，如果左边比较小，则左指针一直往前移动，直到找到一个更大的值。在这中间的这段区域，存水量必然可以确定（因为左边最大值必然比右边最大值小），右指针的行为正好相反。写代码时一定要注意边界条件的判断。时间复杂度`O(n)`并且只需要遍历一次数组，空间复杂度`O(1)`。

## 代码

### 两次遍历法
```python
class Solution(object):
    def trap(self, height):
        """
        :type height: List[int]
        :rtype: int
        """
        max_lefts = []
        cur_max = 0
        for n in height:
            cur_max = max(cur_max, n)
            max_lefts.append(cur_max)
        cur_max = 0
        x = 0
        for i in xrange(len(height) - 1, -1, -1):
            n = height[i]
            cur_max = max(cur_max, n)
            x += min(cur_max, max_lefts[i]) - n
        return x
```

### 两指针法 
```python
class Solution(object):
    def trap(self, height):
        """
        :type height: List[int]
        :rtype: int
        """
        low, high = 0, len(height) - 1
        s = 0
        while low < high:
            if height[low] < height[high]:
                k = low + 1
                while height[k] <= height[low]:
                    s += height[low] - height[k]
                    k += 1
                low = k
            else:
                k = high - 1
                while height[k] < height[high]:
                    s += height[high] - height[k]
                    k -= 1
                high = k
        return s
```
