title: Leetcode解题-Merge Two Sorted Lists
date: 2015-09-10 10:50:42
tags: [Leetcode, 链表, Sorting]
categories: [编程题]
---

## 描述
> Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.

## 分析
和合并两有序数组基本一样，链表操作还会更简单一点。

## 代码
### Python
```python
class Solution(object):
    def mergeTwoLists(self, l1, l2):
        """
        :type l1: ListNode
        :type l2: ListNode
        :rtype: ListNode
        """
        dummy = ListNode(-1)
        dummy.next = l1
        prev = dummy
        while l1 and l2:
            if l1.val > l2.val:
                prev.next = l2
                prev = l2
                l2 = l2.next
            else:
                prev.next = l1
                prev = l1
                l1 = l1.next
        if not l1:
            prev.next = l2
        else:
            prev.next = l1
        return dummy.next
```
