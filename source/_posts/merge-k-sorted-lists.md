title: Leetcode解题-Merge k Sorted Lists
date: 2015-09-10 11:12:24
tags: [Leetcode, 链表, Sorting]
categories: [编程题]
---

## 描述
> Merge k sorted linked lists and return it as one sorted list. Analyze and describe its complexity.

## 分析
和[上一题][1]思路是一样的，不过简单的按顺序合并提交会超时，要想办法加速。空间换时间，利用一个heap，使得找当前最小值从`O(k)`降到`O(logk)`。

## 代码
### K条同时合并（提交会超时）
```python
class Solution(object):
    def argmin(self, lists):
        idx = -1
        min_val = float('inf')
        for i, node in enumerate(lists):
            if node and node.val < min_val:
                idx = i
                min_val = node.val
        return idx

    def mergeKLists(self, lists):
        """
        :type lists: List[ListNode]
        :rtype: ListNode
        """
        dummy = ListNode(-1)
        p = dummy
        while True:
            idx = self.argmin(lists)
            if idx < 0:
                break
            p.next = lists[idx]
            p = p.next
            lists[idx] = lists[idx].next
        return dummy.next
```

### 一个一个合并（仍然超时）
```python
class Solution(object):
    def mergeTwoLists(self, l1, l2):
        """
        :type l1: ListNode
        :type l2: ListNode
        :rtype: ListNode
        """
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

    def mergeKLists(self, lists):
        """
        :type lists: List[ListNode]
        :rtype: ListNode
        """
        if not lists:
            return None
        p = lists[0]
        for l in lists[1:]:
            p = self.mergeTwoLists(p, l)
        return p
```

### 利用heap加速
```python
import heapq


class Solution(object):
    def mergeKLists(self, lists):
        """
        :type lists: List[ListNode]
        :rtype: ListNode
        """
        dummy = ListNode(-1)
        prev = dummy
        heap = []
        for p in lists:
            if p:
                heap.append((p.val, p))
        heapq.heapify(heap)
        while heap:
            # pop min
            val, p = heapq.heappop(heap)
            prev.next = p
            prev = prev.next
            if p.next:
                heapq.heappush(heap, (p.next.val, p.next))
        return dummy.next
```


[1]: /2015/09/10/merge-two-sorted-lists/
