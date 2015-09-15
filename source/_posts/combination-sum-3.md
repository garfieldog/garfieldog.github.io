title: Leetcode解题-Combination Sum III
date: 2015-09-15 19:42:08
tags: [Leetcode, 回溯法, DFS]
categories: [编程题]
---

## 描述
> Find all possible combinations of k numbers that add up to a number n, given that only numbers from 1 to 9 can be used and each combination should be a unique set of numbers.
>
> Ensure that numbers within the set are sorted in ascending order.
>
> Example 1:
>
> Input: k = 3, n = 7
>
> Output:
>
> [[1,2,4]]
>
> Example 2:
>
> Input: k = 3, n = 9
>
> Output:
>
> [[1,2,6], [1,3,5], [2,3,4]]
> Credits:
> Special thanks to @mithmatt for adding this problem and creating all test cases.

## 分析
和[Combination Sum][1]、[Combination Sum II][2]这两道题是一系列的，解法也大同小异。这次多了一个步长。

## 代码
### Python
```python
class Solution(object):
    def dfs(self, candidates, target, k, path, rs):
        if k == 0:
            if target == 0:
                rs.append(path[:])
            return
        for i in xrange(len(candidates)):
            c = i + 1
            if not candidates[i] and (not path or c >= path[-1]) and target - c >= 0:
                path.append(c)
                candidates[i] = 1
                self.dfs(candidates, target - c, k - 1, path, rs)
                path.pop()
                candidates[i] = 0

    def combinationSum3(self, k, n):
        """
        :type k: int
        :type n: int
        :rtype: List[List[int]]
        """
        if n <= 0:
            return []
        rs = []
        path = []
        candidates = [0] * 9
        self.dfs(candidates, n, k, path, rs)
        return rs
```

[1]: /2015/09/15/combination-sum/
[2]: /2015/09/15/combination-sum-2/
