title: Leetcode解题-Remove Duplicates From Sorted List II
date: 2015-08-25 19:27:13
tags: [Leetcode, 链表]
categories: [编程题]
---

## 描述
> Given a sorted linked list, delete all nodes that have duplicate numbers, leaving only distinct numbers from the original list.
>
> For example,
> Given 1->2->3->3->4->4->5, return 1->2->5.
> Given 1->1->1->2->3, return 2->3.

和[Remove Duplicates from Sorted List][1]设定基本一样，要求返回值只包括唯一的元素。

## 分析
需要额外判断删除了重复值后剩下的数是本来就唯一呢，还是曾经有重复值。

## 代码

### Python
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
            dup = False
            while cur.next and cur.val == cur.next.val:
                dup = True
                cur = cur.next
            # now cur is the either an unique number or the last one the a sequence of duplicates
            if not dup:
                prev.next = cur
                prev = prev.next
            cur = cur.next
        prev.next = cur
        return dummy.next
```

[1]: /2015/08/25/remove-duplicates-from-sorted-list/
