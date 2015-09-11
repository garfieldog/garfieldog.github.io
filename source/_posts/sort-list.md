title: Leetcode解题-Sort List
date: 2015-09-11 10:20:07
tags: [Leetcode, 链表, Sorting]
categories: [编程题]
---

## 描述
> Sort a linked list in O(n log n) time using constant space complexity.

## 分析
要求时间`O(nlogn)`，上一题的插入排序就不能用了，可以使用归并排序，先split成两个链表，分别递归排序，再归并。可以用到我们之前的[Merge Two Sorted List][1]。

## 代码
### 归并排序
```python
class Solution(object):
    def mergeTwoLists(self, l1, l2):
        dummy = ListNode(-1)
        dummy.next = l1
        prev = dummy
        while l1 and l2:
            if l1.val > l2.val:
                prev.next = l2
                prev = l2
                l2 = l2.next
            else:
                prev.next = l1
                prev = l1
                l1 = l1.next
        if not l1:
            prev.next = l2
        else:
            prev.next = l1
        return dummy.next

    def splitList(self, head):
        h1 = head
        h2 = head.next
        p1 = h1
        p2 = h2
        while p2:
            p1.next = p2.next
            if p2.next:
                p2.next = p2.next.next
            p1 = p1.next
            p2 = p2.next
        return h1, h2

    def sortList(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        if not head or not head.next:
            return head
        # split to two lists
        l1, l2 = self.splitList(head)
        l1 = self.sortList(l1)
        l2 = self.sortList(l2)
        return self.mergeTwoLists(l1, l2)
```

[1]: /2015/09/10/merge-two-sorted-lists/
