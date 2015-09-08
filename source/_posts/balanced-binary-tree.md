title: Leetcode解题-Balanced Binary Tree
date: 2015-09-08 15:08:23
tags: [Leetcode, Tree]
categories: [编程题]
---

## 描述
> Given a binary tree, determine if it is height-balanced.
>
> For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of every node never differ by more than 1.

## 分析
检查二叉树是否平衡，递归法很简单。

## 代码
### Python
```python
class Solution(object):
    def isBalancedR(self, root):
        if not root:
            return (True, 0)
        f1, h1 = self.isBalancedR(root.left)
        f2, h2 = self.isBalancedR(root.right)
        f = f1 and f2 and abs(h1 - h2) < 2
        return f, max(h1, h2) + 1

    def isBalanced(self, root):
        """
        :type root: TreeNode
        :rtype: bool
        """
        f, h = self.isBalancedR(root)
        return f
```
