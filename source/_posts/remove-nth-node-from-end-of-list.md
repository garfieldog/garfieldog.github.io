title: Leetcode解题-Remove Nth node From End of List
date: 2015-08-26 14:10:04
tags: [Leetcode, 链表, 两指针]
categories: [编程题]
---

## 描述
> Given a linked list, remove the nth node from the end of list and return its head.

> For example,

> Given linked list: 1->2->3->4->5, and n = 2.

> After removing the second node from the end, the linked list becomes 1->2->3->5.
> Note:
> Given n will always be valid.
> Try to do this in one pass.

## 分析
我们在[Rotate List][1]中已经讨论过这个方法，用两指针，时间`O(n)`，空间`O(1)`。

## 代码

### Python
```python
# Definition for singly-linked list.
class ListNode(object):
    def __init__(self, x):
        self.val = x
        self.next = None


class Solution(object):
    def removeNthFromEnd(self, head, n):
        """
        :type head: ListNode
        :type n: int
        :rtype: ListNode
        """
        dummy = ListNode(-1)
        dummy.next = head
        p1 = p2 = dummy
        for i in xrange(n):
            p1 = p1.next

        while p1.next:
            p1 = p1.next
            p2 = p2.next

        p2.next = p2.next.next
        return dummy.next
```

[1]: /2015/08/26/rotate-list/
