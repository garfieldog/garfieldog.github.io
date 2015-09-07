title: Leetcode解题-Binary Tree Inorder Traversal
date: 2015-09-07 15:32:04
tags: [Leetcode, Tree]
categories: [编程题]
---

## 描述
> Given a binary tree, return the inorder traversal of its nodes' values.
>
> For example:
> Given binary tree {1,#,2,3},
>    1
>     \
>      2
>     /
>    3
> return [1,3,2].
>
> Note: Recursive solution is trivial, could you do it iteratively?

## 分析
中序遍历，基本上沿用[上一题][1]的框架。

Morris遍历继续参考[这篇文章][2]。

## 代码
### 递归
```python
class Solution(object):
    def inorderTraversalR(self, root, rs):
        if not root:
            return
        self.inorderTraversalR(root.left, rs)
        rs.append(root.val)
        self.inorderTraversalR(root.right, rs)

    def inorderTraversal(self, root):
        """
        :type root: TreeNode
        :rtype: List[int]
        """
        rs = []
        self.inorderTraversalR(root, rs)
        return rs
```

### 迭代
```python
class Solution(object):
    def inorderTraversal(self, root):
        """
        :type root: TreeNode
        :rtype: List[int]
        """
        rs = []
        ss = []
        cur = root
        while cur or ss:
            if cur:
                ss.append(cur)
                cur = cur.left
            else:
                cur = ss.pop()
                rs.append(cur.val)
                cur = cur.right
        return rs
```

### Morris
```python
class Solution(object):
    def inorderTraversal(self, root):
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
                    node.right = cur
                    cur = cur.left
                else:
                    # already threaded
                    node.right = None
                    rs.append(cur.val)
                    cur = cur.right
        return rs
```

[1]: /2015/09/07/binary-tree-preorder-traversal/
[2]: http://www.cnblogs.com/AnnieKim/archive/2013/06/15/MorrisTraversal.html
