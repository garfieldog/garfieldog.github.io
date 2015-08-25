title: Leetcode解题-Reverse Linked List II 
date: 2015-08-25 15:25:54
tags: [Leetcode, 链表]
categories: [编程题]
---

## 描述
> Reverse a linked list from position m to n. Do it in-place and in one-pass.
>
> For example:
> Given 1->2->3->4->5->NULL, m = 2 and n = 4,
>
> return 1->4->3->2->5->NULL.
>
> Note:
> Given m, n satisfy the following condition:
> 1 ≤ m ≤ n ≤ length of list.

## 分析

要求部分翻转一个链表。看起来不是很难，但要写对真是非常费力。

1. 找到需要翻转的子链表头部的前一个元素`new_head`（为了防止第一个元素没有前一个元素，可以用一个dummy元素插在原链表头部）
2. 从子链表的第二个元素开始遍历子链表，把当前元素插入到`new_head`之后，也就是子链表第一个元素之前，并维护好指针指向。
3. dummy元素之后的链表就是最终结果

## 代码

### Python
```python
# Definition for singly-linked list.
class ListNode(object):
    def __init__(self, x):
        self.val = x
        self.next = None


class Solution(object):
    def reverseBetween(self, head, m, n):
        """
        :type head: ListNode
        :type m: int
        :type n: int
        :rtype: ListNode
        """
        dummy = ListNode(-1)
        dummy.next = head
        prev = dummy
        for i in xrange(m - 1):
            prev = prev.next

        new_head = prev
        prev = new_head.next

        cur = prev.next
        for i in xrange(m, n):
            prev.next = cur.next
            cur.next = new_head.next
            new_head.next = cur
            cur = prev.next

        return dummy.next
```
