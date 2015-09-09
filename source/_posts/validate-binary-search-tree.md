title: Leetcode解题-Validate Binary Search Tree
date: 2015-09-09 14:20:14
tags: [Leetcode, Tree]
categories: [编程题]
---

## 描述
> Given a binary tree, determine if it is a valid binary search tree (BST).
>
> Assume a BST is defined as follows:
>
> The left subtree of a node contains only nodes with keys less than the node's key.
> The right subtree of a node contains only nodes with keys greater than the node's key.
> Both the left and right subtrees must also be binary search trees.

## 分析
检查一个二叉搜索树是不是合法，递归去做，向下传递一个允许的取值范围。时间`O(n)`，空间平均`O(logn)`。

## 代码
### Python
```python
class Solution(object):
    def isValidBSTR(self, root, low, high):
        if not root:
            return True
        if root.val >= high or root.val <= low:
            return False
        if not self.isValidBSTR(root.left, low, root.val):
            return False
        if not self.isValidBSTR(root.right, root.val, high):
            return False
        return True

    def isValidBST(self, root):
        """
        :type root: TreeNode
        :rtype: bool
        """
        return self.isValidBSTR(root, float('-inf'), float('inf'))
```
