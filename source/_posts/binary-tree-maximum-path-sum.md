title: Leetcode解题-Binary Tree Maximum Path Sum
date: 2015-09-09 16:36:51
tags: [Leetcode, Tree]
categories: [编程题]
---

## 描述
> Given a binary tree, find the maximum path sum.
>
> The path may start and end at any node in the tree.
>
> For example:
> Given the below binary tree,
>
>        1
>       / \
>      2   3
> Return 6.

## 分析
题目难度标了`Hard`，其实并不难，关键是要理解最长路径的构成。用深度优先遍历，对于每一个节点，都去考察`以该节点为根，所能构成的最大半条路径`，所谓`半条路径`就是指这条路径上的节点要么都在该节点的左子树，要么都在右子树，没有跨越的情况。这样一来，当前以当前节点为根的最长路径就是把左子树中最长`半条路径`和右子树的最长`半条路径`拼起来。

注意节点的值有可能是负数，所以，如果`半条路径`长是负值，我们就不要它。

## 代码
### Python
```python
class Solution(object):
    max_sum = float('-inf')

    def maxPathSumR(self, root):
        if not root:
            return 0

        s1 = self.maxPathSumR(root.left)
        s2 = self.maxPathSumR(root.right)
        # update max_sum
        self.max_sum = max(s1 + s2 + root.val, s1 + root.val,
                           s2 + root.val, root.val, self.max_sum)
        return max(s1, s2, 0) + root.val

    def maxPathSum(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        self.maxPathSumR(root)
        return self.max_sum
```
