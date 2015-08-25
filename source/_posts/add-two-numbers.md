title: Leetcode解题-Add Two Numbers
date: 2015-08-25 14:08:06
tags: [Leetcode, 链表]
categories: [编程题]
---

## 描述
> You are given two linked lists representing two non-negative numbers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.
>
> Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
> Output: 7 -> 0 -> 8

## 分析
简单的链表题，复用已有链表本身的节点，可以实现时间`O(n)`，空间`O(1)`的算法。


## 代码

### Python
```python
# Definition for singly-linked list.
class ListNode(object):
    def __init__(self, x):
        self.val = x
        self.next = None


class Solution(object):
    def addTwoNumbers(self, l1, l2):
        """
        :type l1: ListNode
        :type l2: ListNode
        :rtype: ListNode
        """
        if l1 is None:
            return l2

        carry = 0
        head = l1
        tail = l1
        while l1 and l2:
            tail = l1
            carry, l1.val = divmod(l1.val + l2.val + carry, 10)
            l1 = l1.next
            l2 = l2.next

        while l1:
            tail = l1
            carry, l1.val = divmod(l1.val + carry, 10)
            l1 = l1.next

        if l2:
            tail.next = l2

        while l2:
            tail = l2
            carry, l2.val = divmod(l2.val + carry, 10)
            l2 = l2.next

        if carry > 0:
            tail.next = ListNode(carry)
        return head
```
