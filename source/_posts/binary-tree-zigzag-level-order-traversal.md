title: Leetcode解题-Binary Tree Zigzag Level Order Traversal
date: 2015-09-07 19:59:30
tags: [Leetcode, Tree]
categories: [编程题]
---

## 描述
> Given a binary tree, return the zigzag level order traversal of its nodes' values. (ie, from left to right, then right to left for the next level and alternate between).
>
> For example:
> Given binary tree {3,9,20,#,#,15,7},
>     3
>    / \
>   9  20
>     /  \
>    15   7
> return its zigzag level order traversal as:
> [
>   [3],
>   [20,9],
>   [15,7]
> ]


## 分析
[Level Order Traveral][1]的姐妹版，要求每一层从左到右、从右到左花插着来。

用一个flag来标识当前level是从左到右还是从右到左，另外在queue中插入行间标示符（这里用`None`）来分割各行。

## 代码
### Python
```python
from collections import deque

class Solution(object):
    def zigzagLevelOrder(self, root):
        """
        :type root: TreeNode
        :rtype: List[List[int]]
        """
        queue = deque()
        level = []
        rs = []
        zig = True
        if not root:
            return []
        queue.append(root)
        queue.append(None)  # None as level seperator
        while queue:
            cur = queue.popleft()
            if cur:
                level.append(cur.val)
                if cur.left:
                    queue.append(cur.left)
                if cur.right:
                    queue.append(cur.right)
            else:
                # level end
                if zig:
                    rs.append(level)
                else:
                    rs.append(level[::-1])
                level = []
                zig = not zig
                if queue:
                    queue.append(None)
        return rs
```


[1]: /2015/09/07/binary-tree-level-order-traversal/
