title: Leetcode解题-Convert Sorted Array to Binary Search Tree
date: 2015-09-09 14:37:40
tags: [Leetcode, Tree]
categories: [编程题]
---

## 描述
> Given an array where elements are sorted in ascending order, convert it to a height balanced BST.

## 分析
递归分治法解很容易，时间`O(n)`，空间平均`O(logn)`。

## 代码
### Python
```python
class Solution(object):
    def sortedArrayToBSTR(self, nums, start, end):
        if start > end:
            return None
        root = (end - start) / 2 + start
        node = TreeNode(nums[root])
        node.left = self.sortedArrayToBSTR(nums, start, root - 1)
        node.right = self.sortedArrayToBSTR(nums, root + 1, end)
        return node

    def sortedArrayToBST(self, nums):
        """
        :type nums: List[int]
        :rtype: TreeNode
        """
        return self.sortedArrayToBSTR(nums, 0, len(nums) - 1)
```
