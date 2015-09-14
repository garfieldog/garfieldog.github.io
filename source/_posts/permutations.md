title: Leetcode解题-Permutations
date: 2015-09-14 10:56:24
tags: [Leetcode, Permutation, DFS]
categories: [编程题]
---

## 描述
> Given a collection of numbers, return all possible permutations.
>
> For example,
> [1,2,3] have the following permutations:
> [1,2,3], [1,3,2], [2,1,3], [2,3,1], [3,1,2], and [3,2,1].

## 分析
我们之前做过一道[Next Permutation][1]的题，稍加改动其实就可以了。还可以深度搜索来做。

## 代码
### Next Permutation
```python
class Solution(object):
    def nextPermutation(self, nums):
        pivot = -1
        for i in xrange(len(nums) - 1, 0, -1):
            if nums[i] > nums[i - 1]:
                pivot = i - 1
                break
        if pivot < 0:
            return False

        for i in xrange(len(nums) - 1, 0, -1):
            if nums[i] > nums[pivot]:
                nums[pivot], nums[i] = nums[i], nums[pivot]
                break

        self.reverse(nums, pivot + 1, len(nums) - 1)
        return True

    def reverse(self, nums, i, j):
        if i >= j:
            return
        t = (j - i + 1) / 2
        for k in xrange(t):
            nums[i + k], nums[j - k] = nums[j - k], nums[i + k]  # swap

    def permute(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        nums.sort()
        rs = []
        while True:
            rs.append(nums[:])
            if not self.nextPermutation(nums):
                break
        return rs
```

### DFS
```python
class Solution(object):
    def dfs(self, nums, path, rs):
        if len(path) == len(nums):
            rs.append(path[:])
            return
        for x in nums:
            if x not in path:
                path.append(x)
                self.dfs(nums, path, rs)
                path.pop()

    def permute(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        rs = []
        path = []
        self.dfs(nums, path, rs)
        return rs
```

[1]: /2015/08/21/next-permutation/
[2]: /2015/08/22/permutation-sequence/
