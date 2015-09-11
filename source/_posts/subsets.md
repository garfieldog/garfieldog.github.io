title: Leetcode解题-Subsets
date: 2015-09-11 16:25:33
tags: [Leetcode, 枚举]
categories: [编程题]
---

## 描述
> Given a set of distinct integers, nums, return all possible subsets.
>
> Note:
> Elements in a subset must be in non-descending order.
> The solution set must not contain duplicate subsets.
> For example,
> If nums = [1,2,3], a solution is:
>
> [
>   [3],
>   [1],
>   [2],
>   [1,2,3],
>   [1,3],
>   [2,3],
>   [1,2],
>   []
> ]

## 分析
生成全部子集，递归很容易，改成迭代也不难，时间`O(2^n)`。

## 代码
### 递归
```python
class Solution(object):
    def subsets(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        if not nums:
            return [[]]
        nums.sort()
        subsets = self.subsets(nums[1:])
        for i in xrange(len(subsets)):
            subsets.append(nums[:1] + subsets[i])
        return subsets
```

### 迭代
```python
class Solution(object):
    def subsets(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        rs = [[]]
        nums.sort(reverse=True)
        for x in nums:
            n = len(rs)
            for i in xrange(n):
                rs.append([x] + rs[i])
        return rs
```
