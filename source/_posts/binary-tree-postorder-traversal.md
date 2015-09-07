title: Leetcode解题-Binary Tree Postorder Traversal
date: 2015-09-07 16:07:48
tags: [Leetcode, Tree]
categories: [编程题]
---

## 描述
> Given a binary tree, return the postorder traversal of its nodes' values.
>
> For example:
> Given binary tree {1,#,2,3},
>    1
>     \
>      2
>     /
>    3
> return [3,2,1].
>
> Note: Recursive solution is trivial, could you do it iteratively?

## 分析
后序遍历是三种遍历中最难的一种，迭代版需要一个额外的指针记录上一个访问过的节点，只有当一个节点左子树和右子树都遍历过后才能访问当前节点，左子树依靠栈来保证（跟中序遍历一样），右子树需要靠prev节点来判断是否访问过。

Morris遍历也要更复杂一些，看[这里][1]。

## 代码
### 递归
```python
class Solution(object):
    def postorderTraversalR(self, root, rs):
        if not root:
            return
        self.postorderTraversalR(root.left, rs)
        self.postorderTraversalR(root.right, rs)
        rs.append(root.val)

    def postorderTraversal(self, root):
        """
        :type root: TreeNode
        :rtype: List[int]
        """
        rs = []
        self.postorderTraversalR(root, rs)
        return rs
```

### 迭代
```python
class Solution(object):
    def postorderTraversal(self, root):
        """
        :type root: TreeNode
        :rtype: List[int]
        """
        rs = []
        ss = []
        cur = root
        prev = None
        while True:
            while cur:
                ss.append(cur)
                cur = cur.left
            prev = None
            while ss:
                cur = ss.pop()
                if cur.right == prev:
                    rs.append(cur.val)
                    prev = cur
                else:
                    ss.append(cur)
                    cur = cur.right
                    break
            if not ss:
                break
        return rs
```

### Morris
```python
class Solution(object):
    def postorderTraversal(self, root):
        """
        :type root: TreeNode
        :rtype: List[int]
        """
        rs = []
        dummy = TreeNode(-1)
        dummy.left = root
        cur = dummy
        while cur:
            if not cur.left:
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
                    # visit left node to predecessor
                    tmp = node
                    self.reverse(cur.left, node)
                    while True:
                        rs.append(tmp.val)
                        if tmp == cur.left:
                            break
                        tmp = tmp.right
                    self.reverse(node, cur.left)
                    cur = cur.right
        return rs

    def reverse(self, a, b):
        if a == b:
            return
        x = a
        y = a.right
        while x != b:
            z = y.right
            y.right = x
            x = y
            y = z
```

[1]: http://www.cnblogs.com/AnnieKim/archive/2013/06/15/MorrisTraversal.html
