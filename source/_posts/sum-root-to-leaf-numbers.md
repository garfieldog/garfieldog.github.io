title: Leetcode解题-Sum Root to Leaf Numbers
date: 2015-09-09 17:09:53
tags: [Leetcode, Tree]
categories: [编程题]
---

## 描述
> Given a binary tree containing digits from 0-9 only, each root-to-leaf path could represent a number.
>
> An example is the root-to-leaf path 1->2->3 which represents the number 123.
>
> Find the total sum of all root-to-leaf numbers.
>
> For example,
>
>     1
>    / \
>   2   3
> The root-to-leaf path 1->2 represents the number 12.
> The root-to-leaf path 1->3 represents the number 13.
>
> Return the sum = 12 + 13 = 25.

## 分析
深度优先遍历，自顶向下传递和值。时间`O(n)`，空间`O(logn)`。

## 代码
### Python
```python
class Solution(object):
    def sumNumbersR(self, root, s):
        if not root:
            return 0
        s = s * 10 + root.val
        if not root.left and not root.right:
            return s

        return self.sumNumbersR(root.left, s) + self.sumNumbersR(root.right, s)

    def sumNumbers(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        return self.sumNumbersR(root, 0)
```
