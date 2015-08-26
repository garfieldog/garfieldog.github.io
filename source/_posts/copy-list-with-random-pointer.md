title: Leetcode解题-Copy List with Random Pointer
date: 2015-08-26 17:51:07
tags: [Leetcode, 链表]
categories: [编程题]
---

## 描述
> A linked list is given such that each node contains an additional random pointer which could point to any node in the list or null.
>
> Return a deep copy of the list.

## 分析
这道题有点技巧，拢共分三步：

1. 第一步，给原链表每个节点复制一个拷贝，插入到原节点后面。
2. 第二步，再次遍历链表，给复制出来的节点设置random指针。
3. 第三步，再次遍历链表，把原链表的节点和复制出来的节点拆成两个链表。

## 代码

### Python
```python
# Definition for singly-linked list with a random pointer.
class RandomListNode(object):
    def __init__(self, x):
        self.label = x
        self.next = None
        self.random = None


class Solution(object):
    def copyRandomList(self, head):
        """
        :type head: RandomListNode
        :rtype: RandomListNode
        """
        if not head:
            return head

        cur = head
        while cur:
            node = RandomListNode(cur.label)
            node.next = cur.next
            cur.next = node
            cur = node.next

        cur = head
        while cur:
            if cur.random:
                cur.next.random = cur.random.next
            cur = cur.next.next

        cur = head
        new_head = cur.next
        while cur and cur.next:
            next = cur.next
            cur.next = cur.next.next
            cur = next
        return new_head
```
