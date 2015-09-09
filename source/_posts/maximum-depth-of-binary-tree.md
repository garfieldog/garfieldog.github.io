title: Leetcode解题-Maximum Depth of Binary Tree
date: 2015-09-09 15:37:38
tags: [Leetcode, Tree]
categories: [编程题]
---

## 描述
> Given a binary tree, find its maximum depth.
>
> The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

## 分析
深度优先遍历可解，时间`O(n)`，空间平均`O(logn)`。

## 代码
### Python
```python
class Solution(object):
    def maxDepth(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        if not root:
            return 0
        d1 = self.maxDepth(root.left)
        d2 = self.maxDepth(root.right)
        return max(d1, d2) + 1
```
