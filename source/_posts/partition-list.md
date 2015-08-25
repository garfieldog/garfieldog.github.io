title: Leetcode解题-Partition List
date: 2015-08-25 17:24:18
tags: [Leetcode, 链表]
categories: [编程题]
---

## 描述

> Given a linked list and a value x, partition it such that all nodes less than x come before nodes greater than or equal to x.
>
> You should preserve the original relative order of the nodes in each of the two partitions.
>
> For example,
> Given 1->4->3->2->5->2 and x = 3,
> return 1->2->2->4->3->5.

## 分析
就是快排中的parition，但使用链表数据结构，实现有一些不一样。维护两个链表，一个把小于x的值串起来，一个把大于等于x的值串起来，最后把这两个链表拼接起来就可以。时间复杂度`O(n)`，空间复杂度`O(1)`。

## 代码

### Python
```python
# Definition for singly-linked list.
class ListNode(object):
    def __init__(self, x):
        self.val = x
        self.next = None


class Solution(object):
    def partition(self, head, x):
        """
        :type head: ListNode
        :type x: int
        :rtype: ListNode
        """
        left_dummy = ListNode(-1)
        right_dummy = ListNode(-1)
        left_cur = left_dummy
        right_cur = right_dummy
        while head:
            if head.val < x:
                left_cur.next = head
                left_cur = head
            else:
                right_cur.next = head
                right_cur = head
            head = head.next

        left_cur.next = right_dummy.next
        right_cur.next = None
        return left_dummy.next
```


