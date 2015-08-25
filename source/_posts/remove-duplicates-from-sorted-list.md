title: Leetcode解题-Remove Duplicates From Sorted List
date: 2015-08-25 19:27:13
tags: [Leetcode, 链表]
categories: [编程题]
---

## 描述
> Given a sorted linked list, delete all duplicates such that each element appear only once.
>
> For example,
> Given 1->1->2, return 1->2.
> Given 1->1->2->3->3, return 1->2->3.

## 分析
我们之前做过一道[Remove Duplicates from Sorted Array][1]，跟这道题解法其实是一样的，只是数据结构换成了链表。注意指针的维护。时间`O(n)`，空间`O(1)`。

## 代码
```python
# Definition for singly-linked list.
class ListNode(object):
    def __init__(self, x):
        self.val = x
        self.next = None


class Solution(object):
    def deleteDuplicates(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        dummy = ListNode(None)
        dummy.next = head
        prev = dummy
        cur = head
        while cur:
            if cur.val == prev.val:
                prev.next = cur.next
                cur = cur.next
            else:
                cur = cur.next
                prev = prev.next
        return dummy.next
```

[1]: /2015/08/18/remove-duplicates-from-sorted-array/
