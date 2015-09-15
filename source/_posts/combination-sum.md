title: Leetcode解题-Combination Sum
date: 2015-09-15 19:16:43
tags: [Leetcode, 回溯法, DFS]
categories: [编程题]
---

## 描述
> Given a set of candidate numbers (C) and a target number (T), find all unique combinations in C where the candidate numbers sums to T.
>
> The same repeated number may be chosen from C unlimited number of times.
>
> Note:
> All numbers (including target) will be positive integers.
> Elements in a combination (a1, a2, … , ak) must be in non-descending order. (ie, a1 ≤ a2 ≤ … ≤ ak).
> The solution set must not contain duplicate combinations.
> For example, given candidate set 2,3,6,7 and target 7, 
> A solution set is: 
> [7] 
> [2, 2, 3] 

## 分析
依然是回溯法，不再解释，注意剪枝条件（保证combination是递增的）

## 代码
### Python
```python
class Solution(object):
    def dfs(self, candidates, target, path, rs):
        if target == 0:
            rs.append(path[:])
            return
        for c in candidates:
            if (not path or c >= path[-1]) and target - c >= 0:
                path.append(c)
                self.dfs(candidates, target - c, path, rs)
                path.pop()

    def combinationSum(self, candidates, target):
        """
        :type candidates: List[int]
        :type target: int
        :rtype: List[List[int]]
        """
        if target <= 0:
            return []
        rs = []
        path = []
        candidates.sort()
        self.dfs(candidates, target, path, rs)
        return rs
```
