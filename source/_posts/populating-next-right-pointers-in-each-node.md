title: Leetcode解题-Populating Next Right Pointers in Each Node
date: 2015-09-09 09:46:14
tags: [Leetcode, Tree, Queue]
categories: [编程题]
---

## 描述
> Given a binary tree
>
>     struct TreeLinkNode {
>       TreeLinkNode *left;
>       TreeLinkNode *right;
>       TreeLinkNode *next;
>     }
> Populate each next pointer to point to its next right node. If there is no next right node, the next pointer should be set to NULL.
>
> Initially, all next pointers are set to NULL.
>
> Note:
>
> You may only use constant extra space.
> You may assume that it is a perfect binary tree (ie, all leaves are at the same level, and every parent has two children).
> For example,
> Given the following perfect binary tree,
>          1
>        /  \
>       2    3
>      / \  / \
>     4  5  6  7
> After calling your function, the tree should look like:
>          1 -> NULL
>        /  \
>       2 -> 3 -> NULL
>      / \  / \
>     4->5->6->7 -> NULL

## 分析
其实就是广度优先遍历，用队列实现。其中用了[Zigzag Level Traversal][1]中的一个技巧，在队列里加入None来分隔各个level。

## 代码
### Python
```python
# Definition for binary tree with next pointer.
class TreeLinkNode(object):
    def __init__(self, x):
        self.val = x
        self.left = None
        self.right = None
        self.next = None


from collections import deque


class Solution(object):
    def connect(self, root):
        """
        :type root: TreeLinkNode
        :rtype: nothing
        """
        if not root:
            return
        q = deque()
        q.append(root)
        q.append(None)
        while q:
            cur = q.popleft()
            if cur:
                if q:
                    cur.next = q[0]
                if cur.left:
                    q.append(cur.left)
                if cur.right:
                    q.append(cur.right)
            else:
                if q:
                    q.append(None)  # level end
```

[1]: /2015/09/07/binary-tree-zigzag-level-order-traversal/
