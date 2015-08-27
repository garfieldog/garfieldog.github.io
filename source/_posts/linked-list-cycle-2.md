title: Leetcode解题-Linked List Cycle II
date: 2015-08-27 22:39:30
tags: [Leetcode, 链表, 两指针]
categories: [编程题]
---

## 描述
> Given a linked list, return the node where the cycle begins. If there is no cycle, return null.
>
> Note: Do not modify the linked list.
>
> Follow up:
> Can you solve it without using extra space?

[Linked List Cycle][1]的升级版。要求不仅判断是否有环，而且要找出环开始的位置。

## 分析
对于存在环的情况，设从链表头部到环第一个元素的距离为`x`，从环第一个元素到两指针相遇点距离为`y`，环长度为`r`。这里可以证明的一点是，当两指针相遇时，慢指针肯定没有跑完一圈。这样来证明：当慢指针到达环第一个元素时，快指针肯定在环中某个地方，设距离环第一个元素`z`，肯定有`z < r`。而快指针只需要`z`步就可以追上慢指针，所以慢指针没有机会跑完一圈。

设相遇时已经走了`t`步，则`t = x + y`, `2t = x + y + nr`， 其中`n`为正整数。则可以推导出`t = nr`，`x = nr - y = (n - 1)r + (r - y)`。这样一来，如果我们在两指针相遇后，再用一个指针从链表头开始走，直到它和慢指针相遇，相遇点就是环开始的地方。

## 代码

### Python
```python
# Definition for singly-linked list.
class ListNode(object):
    def __init__(self, x):
        self.val = x
        self.next = None


class Solution(object):
    def detectCycle(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """

        if not head or not head.next:
            return None

        p1 = head.next
        p2 = head.next.next
        while p2:
            if not p2 or not p2.next:
                return None
            if p1 == p2:
                break
            p2 = p2.next.next
            p1 = p1.next

        if p1 == p2:
            p2 = head
            while p1 != p2:
                p1 = p1.next
                p2 = p2.next
            return p1
```

[1]: /2015/08/27/linked-list-cycle/
