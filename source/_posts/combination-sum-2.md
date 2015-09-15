title: Leetcode解题-Combination Sum II
date: 2015-09-15 19:29:14
tags: [Leetcode, 回溯法, DFS]
categories: [编程题]
---

## 描述
> Given a collection of candidate numbers (C) and a target number (T), find all unique combinations in C where the candidate numbers sums to T.
>
> Each number in C may only be used once in the combination.
>
> Note:
> All numbers (including target) will be positive integers.
> Elements in a combination (a1, a2, … , ak) must be in non-descending order. (ie, a1 ≤ a2 ≤ … ≤ ak).
> The solution set must not contain duplicate combinations.
> For example, given candidate set 10,1,2,7,6,1,5 and target 8, 
> A solution set is: 
> [1, 7] 
> [1, 2, 5] 
> [2, 6] 
> [1, 1, 6] 

## 分析
这次要求一个元素只能用一次（但同样数值的元素可能出现多次，我们用一个OrderedDict来存储计数），稍微修改[Combination Sum][1]中的答案就可以了。

## 代码
### Python
```python
from collections import OrderedDict, Counter


class Solution(object):
    def dfs(self, candidates, target, path, rs):
        if target == 0:
            rs.append(path[:])
            return
        for c, v in candidates.iteritems():
            if v > 0 and (not path or c >= path[-1]) and target - c >= 0:
                path.append(c)
                candidates[c] -= 1
                self.dfs(candidates, target - c, path, rs)
                path.pop()
                candidates[c] += 1

    def combinationSum2(self, candidates, target):
        """
        :type candidates: List[int]
        :type target: int
        :rtype: List[List[int]]
        """
        if target <= 0:
            return []
        rs = []
        path = []
        c = Counter(candidates)
        candidates = OrderedDict(sorted(c.items()))
        self.dfs(candidates, target, path, rs)
        return rs
```

[1]: /2015/09/15/combination-sum/
