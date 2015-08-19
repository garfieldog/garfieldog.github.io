title: Leetcode解题-最长连续序列
date: 2015-08-19 23:51:57
tags: [Leetcode, Array, 哈希表]
categories: [编程题]
---

## 描述

> Given an unsorted array of integers, find the length of the longest consecutive elements sequence.
>
> For example,
> Given [100, 4, 200, 1, 3, 2],
> The longest consecutive elements sequence is [1, 2, 3, 4]. Return its length: 4.
>
> Your algorithm should run in O(n) complexity.

给定一个未排序的整形数组，求出`最长连续元素序列`的长度。比如，给定数组`[100, 4, 200, 1, 3, 2]`，最长连续子序列为`[1, 2, 3, 4]`，长度为4。要求时间复杂度O(n)。

## 分析
要求O(n)时间复杂度，就不能对数组排序，可以尝试用哈希表记录出现的元素。然后第二次遍历原数组，对每个元素，采用从中间向两边扩散的方式查找它的`相邻数`在不在哈希表中，一旦断掉就停止扩张，记录最长的序列长度。注意，要保证时间是O(n)的，就要记录元素有没有被`使用过`，被使用过的元素就不在进行判断，保证一个元素只被访问一次。

## 代码

### Python
```python
class Solution:
    # @param {integer[]} nums
    # @return {integer}
    def longestConsecutive(self, nums):
        d = {n: True for n in nums}
        cur_max_len = 0
        for n in nums:
            if not d.get(n):
                continue
            d[n] = False
            i = 1
            cur_num = n + 1
            while d.get(cur_num):
                d[cur_num] = False
                i += 1
                cur_num += 1
            cur_num = n - 1
            while d.get(cur_num):
                d[cur_num] = False
                i += 1
                cur_num -= 1
            if i > cur_max_len:
                cur_max_len = i
        return cur_max_len
```

