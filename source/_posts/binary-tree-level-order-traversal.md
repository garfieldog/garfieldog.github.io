title: Leetcode解题-Binary Tree Level Order Traversal
date: 2015-09-07 19:34:45
tags: [Leetcode, Tree]
categories: [编程题]
---

## 描述
> Given a binary tree, return the level order traversal of its nodes' values. (ie, from left to right, level by level).
>
> For example:
> Given binary tree {3,9,20,#,#,15,7},
>     3
>    / \
>   9  20
>     /  \
>    15   7
> return its level order traversal as:
> [
>   [3],
>   [9,20],
>   [15,7]
> ]

## 分析
广度优先遍历，用队列实现。

## 代码
### Python
```python
from collections import deque, OrderedDict


# Definition for a binary tree node.
class TreeNode(object):
    def __init__(self, x):
        self.val = x
        self.left = None
        self.right = None


class Solution(object):
    def levelOrder(self, root):
        """
        :type root: TreeNode
        :rtype: List[List[int]]
        """
        queue = deque()
        d = OrderedDict()
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
        return d.values()
```
