title: Leetcode解题-Symmetric Tree
date: 2015-09-08 10:09:11
tags: [Leetcode, Tree]
categories: [编程题]
---

## 描述
> Given a binary tree, check whether it is a mirror of itself (ie, symmetric around its center).
>
> For example, this binary tree is symmetric:
>
>     1
>    / \
>   2   2
>  / \ / \
> 3  4 4  3
> But the following is not:
>     1
>    / \
>   2   2
>    \   \
>    3    3
> Note:
> Bonus points if you could solve it both recursively and iteratively.

## 分析
左右对称地遍历二叉树，递归版比较容易。时间`O(n)`，空间平均`O(logn)`，最坏`O(n)`。

## 代码
### 递归
```python
class Solution(object):
    def isSymmetric(self, root):
        """
        :type root: TreeNode
        :rtype: bool
        """
        return not root or self.isSymmetric2(root.left, root.right)

    def isSymmetric2(self, left, right):
        if not left or not right:
            return left == right
        if left.val != right.val:
            return False
        if not self.isSymmetric2(left.left, right.right):
            return False
        if not self.isSymmetric2(left.right, right.left):
            return False
        return True
```

### 迭代
```python
class Solution(object):
    def isSymmetric(self, root):
        """
        :type root: TreeNode
        :rtype: bool
        """
        if not root:
            return True
        ss = []
        ss.append((root.left, root.right))
        while ss:
            x, y = ss.pop()
            if not x or not y:
                if x == y:
                    continue
                else:
                    return False
            if x.val != y.val:
                return False
            ss.append((x.right, y.left))
            ss.append((x.left, y.right))
        return True
```
