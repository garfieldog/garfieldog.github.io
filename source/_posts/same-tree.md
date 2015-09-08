title: Leetcode解题-Same Tree
date: 2015-09-08 09:49:41
tags: [Leetcode, Tree]
categories: [编程题]
---

## 描述
> Given two binary trees, write a function to check if they are equal or not.
>
> Two binary trees are considered equal if they are structurally identical and the nodes have the same value.

## 分析
本质上就是遍历二叉树，递归法很简单，迭代也不难写。时间`O(n)`，空间平均`O(logn)`，最坏`O(n)`。

## 代码
### 递归
```python
class Solution(object):
    def isSameTree(self, p, q):
        """
        :type p: TreeNode
        :type q: TreeNode
        :rtype: bool
        """
        if not p or not q:
            return p == q

        if p.val != q.val:
            return False
        if not self.isSameTree(p.left, q.left):
            return False
        if not self.isSameTree(p.right, q.right):
            return False
        return True
```

### 迭代
```python
class Solution(object):
    def isSameTree(self, p, q):
        """
        :type p: TreeNode
        :type q: TreeNode
        :rtype: bool
        """
        # preorder traversal
        ss = []
        ss.append((p, q))
        while ss:
            x, y = ss.pop()
            if (not x or not y):
                if x == y:
                    continue
                else:
                    return False
            if x.val != y.val:
                return False
            ss.append((x.right, y.right))
            ss.append((x.left, y.left))
        return True
```


