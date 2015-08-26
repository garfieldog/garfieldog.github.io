title: Leetcode解题-Reverse Nodes in k-Group
date: 2015-08-26 15:00:29
tags: [Leetcode, 链表]
categories: [编程题]
---

## 描述
> Given a linked list, reverse the nodes of a linked list k at a time and return its modified list.
>
> If the number of nodes is not a multiple of k then left-out nodes in the end should remain as it is.
>
> You may not alter the values in the nodes, only nodes itself may be changed.
>
> Only constant memory is allowed.
>
> For example,
> Given this linked list: 1->2->3->4->5
>
> For k = 2, you should return: 2->1->4->3->5
>
> For k = 3, you should return: 3->2->1->4->5

## 分析
[Swap Nodes in Pairs][1]的升级版。一组一组地翻转，注意指针操作。

## 代码

### Python
```python
# Definition for singly-linked list.
class ListNode(object):
    def __init__(self, x):
        self.val = x
        self.next = None


class Solution(object):
    def reverse(self, prev, end, k):
        end_next = end.next
        head = prev.next
        p1 = head
        p2 = head.next
        while p2 != end_next:
            next = p2.next
            p2.next = p1
            p1 = p2
            p2 = next
        head.next = end_next
        prev.next = p1
        return head

    def reverseKGroup(self, head, k):
        """
        :type head: ListNode
        :type k: int
        :rtype: ListNode
        """
        if not head or not head.next or k < 2:
            return head

        dummy = ListNode(-1)
        dummy.next = head
        prev = dummy
        while head:
            end = head
            for i in xrange(k - 1):
                if end:
                    end = end.next
            if not end:  # not enough k nodes
                break
            prev = self.reverse(prev, end, k)
            head = prev.next
        return dummy.next
```

[1]: /2015/08/26/swap-nodes-in-pairs/
