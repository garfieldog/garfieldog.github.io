title: Leetcode解题-Binary Tree Level Order Traversal II
date: 2015-09-07 19:49:25
tags: [Leetcode, Tree]
categories: [编程题]
---

## 描述
> Given a binary tree, return the bottom-up level order traversal of its nodes' values. (ie, from left to right, level by level from leaf to root).
>
> For example:
> Given binary tree {3,9,20,#,#,15,7},
>     3
>    / \
>   9  20
>     /  \
>    15   7
> return its bottom-up level order traversal as:
> [
>   [15,7],
>   [9,20],
>   [3]
> ]

## 分析
[Level Order Traveral][1]的姐妹版，要求最底层的先输出。

## 代码
### Python
```python
from collections import deque


# Definition for a binary tree node.
class TreeNode(object):
    def __init__(self, x):
        self.val = x
        self.left = None
        self.right = None


class Solution(object):
    def levelOrderBottom(self, root):
        """
        :type root: TreeNode
        :rtype: List[List[int]]
        """
        queue = deque()
        d = {}
        if not root:
            return []
        queue.append((root, 0))
        while queue:
            cur, idx = queue.popleft()
            d.setdefault(idx, []).append(cur.val)
            if cur.left:
                queue.append((cur.left, idx + 1))
            if cur.right:
                queue.append((cur.right, idx + 1))
        return [v for k, v in sorted(d.items(), key=lambda x: -x[0])]
```

[1]: /2015/09/07/binary-tree-level-order-traversal/
