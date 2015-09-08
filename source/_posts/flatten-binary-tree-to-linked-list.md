title: Leetcode解题-Flatten Binary Tree to Linked List
date: 2015-09-08 16:13:19
tags: [Leetcode, Tree]
categories: [编程题]
---

## 描述
> Given a binary tree, flatten it to a linked list in-place.
>
> For example,
> Given
>
>          1
>         / \
>        2   5
>       / \   \
>      3   4   6
> The flattened tree should look like:
>    1
>     \
>      2
>       \
>        3
>         \
>          4
>           \
>            5
>             \
>              6
> Hints:
> If you notice carefully in the flattened tree, each node's right child points to the next node of a pre-order traversal.

## 分析
这道题有点莫名其妙，不知道初衷是什么。按照提示，先序遍历，把每个被访问的节点右儿子设为下一个要访问的节点。迭代法用栈实现，时间`O(n)`，空间`O(logn)`。

## 代码
### Python
```python
class Solution(object):
    def flatten(self, root):
        """
        :type root: TreeNode
        :rtype: void Do not return anything, modify root in-place instead.
        """
        # preorder traversal
        ss = []
        if root:
            ss.append(root)
        while ss:
            cur = ss.pop()
            if cur.right:
                ss.append(cur.right)
            if cur.left:
                ss.append(cur.left)
            # visit cur
            cur.left = None
            if ss:
                cur.right = ss[-1]
```
