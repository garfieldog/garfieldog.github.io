title: Leetcode解题-Rotate List
date: 2015-08-26 10:20:17
tags: [Leetcode, 链表]
categories: [编程题]
---

## 描述
> Given a list, rotate the list to the right by k places, where k is non-negative.
>
> For example:
> Given 1->2->3->4->5->NULL and k = 2,
> return 4->5->1->2->3->NULL.

## 分析
同样看上去不难，但要写对还是不容易。首先要解决找到右手起第k个数，这个有一个精妙的找法，用两个指针，一个先走k步，然后两个一起走，第一个指针到尾部时，第二个指针恰好就在倒数第k个位置。但这道题k有可能比链表长度大，所以用这种方法就没意义了，还是老老实实遍历一遍列表数出个数吧。

1. 遍历列表获得总长度，将右手第k转化为左手第`(len - k) % len`个。
2. 这时候有一个比较巧的做法，就是先把列表首尾连接起来（我们第一次遍历结束时指针恰好在尾部）。
3. 然后让指针继续走`(len - k) % len`步，这时候就走到了新链表的尾部，断开环，返回新头部。

## 代码

### Python
```python
# Definition for singly-linked list.
class ListNode(object):
    def __init__(self, x):
        self.val = x
        self.next = None


class Solution(object):
    def rotateRight(self, head, k):
        """
        :type head: ListNode
        :type k: int
        :rtype: ListNode
        """
        if not head or k == 0:
            return head
        cur = head
        length = 1
        while cur.next:
            length += 1
            cur = cur.next
        k = (length - k) % length
        # now cur is the last element
        cur.next = head
        for i in xrange(k):
            cur = cur.next
        new_head = cur.next
        cur.next = None
        return new_head
```
