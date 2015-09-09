title: Leetcode解题-Construct Binary Tree from Preorder and Inorder Traversal
date: 2015-09-09 10:57:25
tags: [Leetcode, Tree]
categories: [编程题]
---

## 描述
> Given preorder and inorder traversal of a tree, construct the binary tree.
>
> Note:
> You may assume that duplicates do not exist in the tree.

## 分析
经典题，从前序遍历和中序遍历重建二叉树。前序遍历的第一个节点肯定是root，在中序遍历中查找root，可以把中序遍历分为两部分，root前面的是左子树的中序遍历，后面的是右子树的中序遍历。对应地，也可以确定前序遍历左子树和右子树的分界（通过中序遍历左子树的大小），这样递归可解。

时间`O(n)`，空间平均`O(logn)`。

## 代码
### Python
```python
class Solution(object):
    def buildTreeR(self, preorder, x1, y1, inorder, x2, y2):
        if x1 > y1:
            return None
        if x2 > y2:
            return None

        node = TreeNode(preorder[x1])
        root_idx = inorder.index(preorder[x1])
        left_size = root_idx - x2
        node.left = self.buildTreeR(preorder, x1 + 1, x1 + left_size,
                                    inorder, x2, root_idx - 1)
        node.right = self.buildTreeR(preorder, x1 + left_size + 1, y1,
                                     inorder, root_idx + 1, y2)
        return node

    def buildTree(self, preorder, inorder):
        """
        :type preorder: List[int]
        :type inorder: List[int]
        :rtype: TreeNode
        """
        return self.buildTreeR(preorder, 0, len(preorder) - 1,
                               inorder, 0, len(inorder) - 1)
```
