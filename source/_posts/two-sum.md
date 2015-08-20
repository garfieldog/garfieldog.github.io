title: Leetcode解题-Two Sum
date: 2015-08-20 10:57:43
tags: [Leetcode, Array, 哈希表]
categories: [编程题]
---

## 描述

> Given an array of integers, find two numbers such that they add up to a specific target number.
>
> The function twoSum should return indices of the two numbers such that they add up to the target, where index1 must be less than index2. Please note that your returned answers (both index1 and index2) are not zero-based.
>
> You may assume that each input would have exactly one solution.
>
> Input: numbers={2, 7, 11, 15}, target=9
> Output: index1=1, index2=2

## 分析
简单的做法就是用哈希表存储数字和它在数组中的下标，然后扫描一遍数组即可。时间复杂度O(n)，空间复杂度O(n)。题目中没有说明数组中有没有重复，如果有重复的数字这个算法还有效吗？乍一看是不对的，但其实仍然是有效的，因为构建哈希表我们是按照数组顺序遍历的，所以如果一个数字出现在多个位置，那哈希表中它存储的下标一定是最大的那个，这样一来，第二次扫描数组，如果`target = 2 * A[i]`，在哈希表中查找`A[i]`，得到的下标`j`一定大于`i`。

## 代码

### Python
```python
class Solution:
    # @return a tuple, (index1, index2)
    def twoSum(self, nums, target):
        d = {x: i for i, x in enumerate(nums)}
        for i, x in enumerate(nums):
            j = d.get(target - x)
            if j and j > i:  # notice: the condition is important
                return (i + 1, j + 1)
```
