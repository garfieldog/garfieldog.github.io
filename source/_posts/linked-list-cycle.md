title: Leetcode解题-Linked List Cycle
date: 2015-08-27 22:25:31
tags: [Leetcode, 链表, 两指针]
categories: [编程题]
---

## 描述
> Given a linked list, determine if it has a cycle in it.
>
> Follow up:
> Can you solve it without using extra space?

## 分析
经典题，使用两指针，一个每次走一步，另一个走两步，如果两指针相遇，则说明有环。

## 代码

### Python
```python
# Definition for singly-linked list.
class ListNode(object):
    def __init__(self, x):
        self.val = x
        self.next = None


class Solution(object):
    def hasCycle(self, head):
        """
        :type head: ListNode
        :rtype: bool
        """
        if not head or not head.next:
            return False

        p1 = head.next
        p2 = head.next.next
        while p2:
            if not p2 or not p2.next:
                return False
            if p1 == p2:
                return True
            p2 = p2.next.next
            p1 = p1.next
        return False
```
