title: Leetcode解题-Recover Binary Search Tree
date: 2015-09-07 22:17:30
tags: [Leetcode, Tree]
categories: [编程题]
---

## 描述
> Two elements of a binary search tree (BST) are swapped by mistake.
>
> Recover the tree without changing its structure.
>
> Note:
> A solution using O(n) space is pretty straight forward. Could you devise a constant space solution?

## 分析
可以用中序遍历来做，记录上一个访问的元素，如果发现违反了正序则记录位置，遍历完之后把两个位置元素调换。时间`O(n)`，空间平均`O(logn)`，最坏`O(n)`。

追求空间`O(1)`的解法可以使用Morris遍历。

## 代码
### 普通中序遍历
```python
class Solution(object):
    def recoverTree(self, root):
        """
        :type root: TreeNode
        :rtype: void Do not return anything, modify root in-place instead.
        """
        # inorder traversal
        cur = root
        ss = []
        prev = TreeNode(float('-inf'))
        first = second = None
        while ss or cur:
            if cur:
                ss.append(cur)
                cur = cur.left
            else:
                cur = ss.pop()
                # visit cur
                if cur.val < prev.val:
                    if not first:
                        first = prev
                    second = cur
                prev = cur
                cur = cur.right
        first.val, second.val = second.val, first.val
```

### Morris遍历
```python
class Solution(object):
    def recoverTree(self, root):
        """
        :type root: TreeNode
        :rtype: void Do not return anything, modify root in-place instead.
        """
        # inorder traversal
        cur = root
        prev = None
        first = second = None
        while cur:
            if not cur.left:
                # visit cur
                if prev and cur.val < prev.val:
                    if not first:
                        first = prev
                    second = cur
                prev = cur
                cur = cur.right
            else:
                node = cur.left
                while node.right and node.right != cur:
                    node = node.right
                if not node.right:
                    # not threaded yet
                    node.right = cur
                    cur = cur.left
                else:
                    # already threaded
                    node.right = None
                    # visit cur
                    if prev and cur.val < prev.val:
                        if not first:
                            first = prev
                        second = cur
                    prev = cur
                    cur = cur.right

        first.val, second.val = second.val, first.val
```
