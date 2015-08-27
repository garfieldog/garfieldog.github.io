title: Leetcode解题-Reorder List
date: 2015-08-27 23:35:15
tags: [Leetcode, 链表]
categories: [编程题]
---

## 描述
> Given a singly linked list L: L0→L1→…→Ln-1→Ln,
> reorder it to: L0→Ln→L1→Ln-1→L2→Ln-2→…
>
> You must do this in-place without altering the nodes' values.
>
> For example,
> Given {1,2,3,4}, reorder it to {1,4,2,3}.

## 分析
分四步：

1. 遍历链表获得长度
2. 找到链表中点，断开成两个链表
3. 翻转第二个链表
4. 将两个链表合并

时间复杂度`O(n)`，空间`O(1)`。

## 代码

### Python
```python
# Definition for singly-linked list.
class ListNode(object):
    def __init__(self, x):
        self.val = x
        self.next = None


class Solution(object):
    def reorderList(self, head):
        """
        :type head: ListNode
        :rtype: void Do not return anything, modify head in-place instead.
        """
        if not head or not head.next:
            return

        l = 0
        cur = head
        while cur:
            l += 1
            cur = cur.next
        m = (l - 1) / 2

        cur = head
        for i in xrange(m):
            cur = cur.next

        head2 = cur.next
        cur.next = None

        # now we have two lists, reverse the second one
        prev = head2
        cur = head2.next
        prev.next = None
        while cur:
            next = cur.next
            cur.next = prev
            prev = cur
            cur = next
        head2 = prev

        # then we merge the two lists
        while head2:
            n1 = head.next
            n2 = head2.next
            head.next = head2
            head2.next = n1
            head = n1
            head2 = n2
```
