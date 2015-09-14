title: Leetcode解题-Permutations II
date: 2015-09-14 11:49:16
tags: [Leetcode, Permutation]
categories: [编程题]
---

## 描述
> Given a collection of numbers that might contain duplicates, return all possible unique permutations.
>
> For example,
> [1,1,2] have the following unique permutations:
> [1,1,2], [1,2,1], and [2,1,1].

## 分析
这次数组中有重复值，用`next permutation`法的话，上一题[Permutations][1]的答案可以直接用。DFS的话要判断当前元素被用了几次。

## 代码
### Next Permutation
见[Permutations][1]。

### DFS
```python
class Solution(object):
    def dfs(self, items, n, path, rs):
        if n == len(path):
            rs.append(path[:])
            return
        for k, v in items:
            c = path.count(k)
            if c < v:
                path.append(k)
                self.dfs(items, n, path, rs)
                path.pop()

    def permuteUnique(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        nums.sort()
        count = {}
        for x in nums:
            count.setdefault(x, 0)
            count[x] += 1
        rs = []
        path = []
        n = len(nums)
        items = count.items()
        self.dfs(items, n, path, rs)
        return rs
```


[1]: /2015/09/14/permutations/
