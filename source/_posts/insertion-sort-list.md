title: Leetcode解题-Insertion Sort List
date: 2015-09-10 22:06:16
tags: [Leetcode, 链表, Sorting]
categories: [编程题]
---

## 描述
> Sort a linked list using insertion sort.

## 分析
链表的插入排序，不难，但程序写对不容易。 

## 代码
### 总是超时的解，发誓逻辑是对的
```python
class Solution(object):
    def insertionSortList(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        if not head:
            return head
        dummy = ListNode(0)
        dummy.next = head
        cur = head
        while cur.next:
            pre = dummy
            while pre != cur and pre.next.val < cur.next.val:
                pre = pre.next
            if pre == cur:
                cur = cur.next
            else:
                next = cur.next
                cur.next = cur.next.next
                next.next = pre.next
                pre.next = next
        return dummy.next
```

### 针对已排序情况做优化
```python
class Solution(object):
    def insertionSortList(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        if not head:
            return head
        dummy = ListNode(0)
        dummy.next = head
        cur = head
        while cur.next:
            if cur.next.val < cur.val:
                pre = dummy
                while pre != cur and pre.next.val < cur.next.val:
                    pre = pre.next
                if pre == cur:
                    cur = cur.next
                else:
                    next = cur.next
                    cur.next = cur.next.next
                    next.next = pre.next
                    pre.next = next
            else:
                cur = cur.next
        return dummy.next
```


