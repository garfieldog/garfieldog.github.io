title: Leetcode解题-Construct Binary Tree from Inorder and Postorder Traversal
date: 2015-09-09 11:26:42
tags: [Leetcode, Tree]
categories: [编程题]
---

## 描述
> Given inorder and postorder traversal of a tree, construct the binary tree.
>
> Note:
> You may assume that duplicates do not exist in the tree.

## 分析
[上一题][1]的姐妹版。如法炮制即可。

PS: 从preorder和postorder是无法重建二叉树的。


## 代码
### Python
```python
class Solution(object):
    def buildTreeR(self, inorder, x1, y1, postorder, x2, y2):
        if x1 > y1:
            return None
        if x2 > y2:
            return None

        node = TreeNode(postorder[y2])
        root_idx = inorder.index(postorder[y2], x1, y1 + 1)
        left_size = root_idx - x1
        node.left = self.buildTreeR(inorder, x1, root_idx - 1,
                                    postorder, x2, x2 + left_size - 1)
        node.right = self.buildTreeR(inorder, root_idx + 1, y1,
                                     postorder, x2 + left_size, y2 - 1)
        return node

    def buildTree(self, inorder, postorder):
        """
        :type inorder: List[int]
        :type postorder: List[int]
        :rtype: TreeNode
        """
        return self.buildTreeR(inorder, 0, len(inorder) - 1,
                               postorder, 0, len(postorder) - 1)
```

[1]: /2015/09/09/construct-binary-tree-from-preorder-and-inorder/
