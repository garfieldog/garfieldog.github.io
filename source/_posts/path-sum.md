title: Leetcode解题-Path Sum
date: 2015-09-09 15:47:07
tags: [Leetcode, Tree]
categories: [编程题]
---

## 描述
> Given a binary tree and a sum, determine if the tree has a root-to-leaf path such that adding up all the values along the path equals the given sum.
>
> For example:
> Given the below binary tree and sum = 22,
>               5
>              / \
>             4   8
>            /   / \
>           11  13  4
>          /  \      \
>         7    2      1
> return true, as there exist a root-to-leaf path 5->4->11->2 which sum is 22.

## 分析
深度优先遍历可解，时间`O(n)`，空间`O(logn)`。

## 代码
### Python
```python
class Solution(object):
    def hasPathSum(self, root, sum):
        """
        :type root: TreeNode
        :type sum: int
        :rtype: bool
        """
        if not root:
            return False
        if not root.left and not root.right:
            return root.val == sum

        return self.hasPathSum(root.left, sum - root.val) or \
            self.hasPathSum(root.right, sum - root.val)
```
