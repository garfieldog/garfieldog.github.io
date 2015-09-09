title: Leetcode解题-Minimum Depth of Binary Tree
date: 2015-09-09 15:23:08
tags: [Leetcode, Tree]
categories: [编程题]
---

## 描述
> Given a binary tree, find its minimum depth.
>
> The minimum depth is the number of nodes along the shortest path from the root node down to the nearest leaf node.

## 分析
广度优先遍历可解，找到第一个叶子节点停止搜索返回高度。时间`O(n)`，空间`O(n)`。

## 解题
### Python
```python
class Solution(object):
    def minDepth(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        q = deque()
        depth = 0
        if root:
            depth += 1
            q.append(root)
            q.append(None)
        while q:
            cur = q.popleft()
            if cur:
                if not cur.left and not cur.right:
                    # leaf node
                    return depth
                if cur.left:
                    q.append(cur.left)
                if cur.right:
                    q.append(cur.right)
            else:
                if q:
                    depth += 1
                    q.append(None)
        return depth
```
