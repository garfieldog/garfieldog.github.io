title: Leetcode解题-Path Sum II
date: 2015-09-09 16:00:01
tags: [Leetcode, Tree]
categories: [编程题]
---

## 描述
> Given a binary tree and a sum, find all root-to-leaf paths where each path's sum equals the given sum.
>
> For example:
> Given the below binary tree and sum = 22,
>               5
>              / \
>             4   8
>            /   / \
>           11  13  4
>          /  \    / \
>         7    2  5   1
> return
> [
>    [5,4,11,2],
>    [5,8,4,5]
> ]

## 分析
比[Path Sum][1]更进一步，要求把符合要求的路径都记下来。

## 代码
### Python
```python
class Solution(object):
    def pathSum(self, root, sum):
        """
        :type root: TreeNode
        :type sum: int
        :rtype: List[List[int]]
        """
        rs = []
        ss = []
        if root:
            ss.append((root, sum, []))
        while ss:
            cur, n, l = ss.pop()
            if not cur.left and not cur.right:
                if n == cur.val:
                    rs.append(l + [cur.val])
            if cur.right:
                ss.append((cur.right, n - cur.val, l + [cur.val]))
            if cur.left:
                ss.append((cur.left, n - cur.val, l + [cur.val]))
        return rs
```

[1]: /2015/09/09/path-sum/
