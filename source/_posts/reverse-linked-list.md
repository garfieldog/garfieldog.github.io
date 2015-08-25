title: Leetcode解题-Reverse Linked List
date: 2015-08-25 15:17:23
tags: [Leetcode, 链表]
categories: [编程题]
---

## 描述
> Reverse a singly linked list.

## 分析
简单题，翻转单链表。时间`O(n)`，空间`O(1)`。

## 代码

### Python
```python
# Definition for singly-linked list.
class ListNode(object):
    def __init__(self, x):
        self.val = x
        self.next = None


class Solution(object):
    def reverseList(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        last = None
        while head:
            next = head.next
            head.next = last
            last = head
            head = next
        return last
```
