title: Leetcode解题-Convert Sorted List to Binary Search Tree
date: 2015-09-09 14:57:02
tags: [Leetcode, Tree]
categories: [编程题]
---

## 描述
> Given a singly linked list where elements are sorted in ascending order, convert it to a height balanced BST.

## 分析
和[上一题][1]不同的是，这次是链表，不能随机访问，那么自顶向下的分治法就失效了。不过可以稍作改动，就可以实现自底向上的构建，需要维护一个全局变量。时间`O(n)`，空间平均`O(logn)`。

## 代码
### Python
```python
class Solution(object):
    cur = None

    def sortedListToBSTR(self, start, end):
        if start > end:
            return None
        root = (end - start) / 2 + start
        left = self.sortedListToBSTR(start, root - 1)
        # now `self.cur` is root
        node = TreeNode(self.cur.val)
        self.cur = self.cur.next
        right = self.sortedListToBSTR(root + 1, end)
        node.left = left
        node.right = right
        return node

    def sortedListToBST(self, head):
        """
        :type head: ListNode
        :rtype: TreeNode
        """
        self.cur = head
        n = 0
        while head:
            n += 1
            head = head.next
        return self.sortedListToBSTR(0, n - 1)
```

[1]: /2015/09/09/convert-sorted-array-to-binary-search-tree/
