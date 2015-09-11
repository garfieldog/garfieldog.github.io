title: Leetcode解题-Subsets II
date: 2015-09-11 16:38:32
tags: [Leetcode, 枚举]
categories: [编程题]
---

## 描述
> Given a collection of integers that might contain duplicates, nums, return all possible subsets.
>
> Note:
> Elements in a subset must be in non-descending order.
> The solution set must not contain duplicate subsets.
> For example,
> If nums = [1,2,2], a solution is:
>
> [
>   [2],
>   [1],
>   [1,2,2],
>   [2,2],
>   [1,2],
>   []
> ]

## 分析
和[Subsets][1]做法基本一样，只是要注意去掉多余的子集。这里采用的方法是，判断当前元素是否和上个元素相等，如果相等，则只扩展上次添加了的子集们，如果不等，就扩展全部。

## 代码
### Python
```python
class Solution:
    # @param {integer[]} nums
    # @return {integer[][]}
    def subsetsWithDup(self, nums):
        rs = [[]]
        nums.sort(reverse=True)
        n = len(nums)
        last_s = 0
        for i in xrange(n):
            s = len(rs)
            start = last_s if i > 0 and nums[i] == nums[i - 1] else 0
            for j in xrange(start, s):
                rs.append([nums[i]] + rs[j])
            last_s = s
        return rs
```

[1]: /2015/09/11/subsets/
