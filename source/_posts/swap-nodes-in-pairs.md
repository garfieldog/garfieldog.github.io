title: Leetcode解题-Swap Nodes In Pairs
date: 2015-08-26 14:34:09
tags: [Leetcode, 链表]
categories: [编程题]
---

## 描述
> Given a linked list, swap every two adjacent nodes and return its head.
>
> For example,
> Given 1->2->3->4, you should return the list as 2->1->4->3.
>
> Your algorithm should use only constant space. You may not modify the values in the list, only nodes itself can be changed.

## 分析
遍历链表，隔一个数（分奇偶）把当前数插到它前一个数的前面。时间`O(n)`，空间`O(1)`。

## 实现

### Python
```python
# Definition for singly-linked list.
class ListNode(object):
    def __init__(self, x):
        self.val = x
        self.next = None


class Solution(object):
    def swapPairs(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        dummy1 = ListNode(-1)
        dummy2 = ListNode(-1)
        dummy1.next = dummy2
        dummy2.next = head
        i = 0
        prev = dummy1
        cur = head
        while cur:
            if i % 2:
                next = cur.next
                prev.next.next = cur.next
                cur.next = prev.next
                prev.next = cur
                cur = next
                prev = prev.next
            else:
                cur = cur.next
                prev = prev.next
            i += 1
        return dummy2.next
```
