title: Leetcode解题-Binary Tree Preorder Traversal
date: 2015-09-07 15:00:02
tags: [Leetcode, Tree]
categories: [编程题]
---

## 描述
> Given a binary tree, return the preorder traversal of its nodes' values.
>
> For example:
> Given binary tree {1,#,2,3},
>    1
>     \
>      2
>     /
>    3
> return [1,2,3].
>
> Note: Recursive solution is trivial, could you do it iteratively?

## 分析
简单题，二叉树的先序遍历。当使用迭代方法时，注意入栈的顺序，需要先push右节点，再push左节点。

还有一种不常用的方法[Morris遍历][1]，可以做到空间`O(1)`，时间`O(n)`。

## 代码
### 递归
```python
# Definition for a binary tree node.
class TreeNode(object):
    def __init__(self, x):
        self.val = x
        self.left = None
        self.right = None


class Solution(object):
    def preorderTraversalR(self, root, rs):
        if not root:
            return
        rs.append(root.val)
        self.preorderTraversalR(root.left, rs)
        self.preorderTraversalR(root.right, rs)

    def preorderTraversal(self, root):
        """
        :type root: TreeNode
        :rtype: List[int]
        """
        rs = []
        self.preorderTraversalR(root, rs)
        return rs
```

### 迭代
```python
# Definition for a binary tree node.
class TreeNode(object):
    def __init__(self, x):
        self.val = x
        self.left = None
        self.right = None


class Solution(object):
    def preorderTraversal(self, root):
        """
        :type root: TreeNode
        :rtype: List[int]
        """
        rs = []
        ss = []
        if root:
            ss.append(root)
        while ss:
            cur = ss.pop()
            rs.append(cur.val)
            if cur.right:
                ss.append(cur.right)
            if cur.left:
                ss.append(cur.left)
        return rs
```

### Morris
```python
# Definition for a binary tree node.
class TreeNode(object):
    def __init__(self, x):
        self.val = x
        self.left = None
        self.right = None


class Solution(object):
    def preorderTraversal(self, root):
        """
        :type root: TreeNode
        :rtype: List[int]
        """
        rs = []
        cur = root
        while cur:
            if not cur.left:
                rs.append(cur.val)
                cur = cur.right
            else:
                # look up predecessor in left sub-tree
                node = cur.left
                while node.right and node.right != cur:
                    node = node.right
                if not node.right:
                    # make threaded
                    rs.append(cur.val)
                    node.right = cur
                    cur = cur.left
                else:
                    # already threaded
                    node.right = None
                    cur = cur.right
        return rs

```

[1]: http://www.cnblogs.com/AnnieKim/archive/2013/06/15/MorrisTraversal.html
