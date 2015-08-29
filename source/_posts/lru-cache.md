title: Leetcode解题-LRU Cache
date: 2015-08-29 17:50:57
tags: [Leetcode, 链表, 哈希表, 数据结构]
categories: [编程题]
---

## 描述
> Design and implement a data structure for Least Recently Used (LRU) cache. It should support the following operations: get and set.
>
> get(key) - Get the value (will always be positive) of the key if the key exists in the cache, otherwise return -1.
> set(key, value) - Set or insert the value if the key is not already present. When the cache reached its capacity, it should invalidate the least recently used item before inserting a new item.

## 分析
要求实现一个LRU cache，有两个要点：

1. `get`, `set`操作都应该是`O(1)`的，否则就失去了cache的意义
2. 要保持LRU的语义

所以我们用一个哈希表外加一个双向链表完成（单项链表无法做到`O(1)`）。用hash表来迅速定位到节点，每次访问一个节点后，将这个节点移动到链表头部(`move_to_head`)，当cache到达capacity上限时，从链表尾部删除节点。

## 代码

### Python
```python
# Definition for singly-linked list.
class ListNode(object):
    def __init__(self, key, val):
        self.key = key
        self.val = val
        self.next = None
        self.prev = None

    def __repr__(self):
        return str(self.val)


class LRUCache(object):

    def __init__(self, capacity):
        """
        :type capacity: int
        """
        self.capacity = capacity
        self.size = 0
        self.dummy_head = ListNode(None, -1)
        self.dummy_tail = ListNode(None, -1)
        self.dummy_head.next = self.dummy_tail
        self.dummy_tail.prev = self.dummy_head
        self.store = {}

    def print_list(self):
        cur = self.dummy_head.next
        while cur != self.dummy_tail:
            print cur.val, '->',
            cur = cur.next
        print

    def move_to_head(self, node):
        if node == self.dummy_head or node == self.dummy_tail:
            return
        if node.prev:
            node.prev.next = node.next
        if node.next:
            node.next.prev = node.prev
        node.prev = self.dummy_head
        node.next = self.dummy_head.next
        self.dummy_head.next.prev = node
        self.dummy_head.next = node

    def get(self, key):
        """
        :rtype: int
        """
        node = self.store.get(key, self.dummy_head)
        self.move_to_head(node)
        return node.val

    def set(self, key, value):
        """
        :type key: int
        :type value: int
        :rtype: nothing
        """
        if key in self.store:
            node = self.store[key]
            node.val = value
            self.move_to_head(node)
        elif self.size < self.capacity:
            node = ListNode(key, value)
            self.move_to_head(node)
            self.store[key] = node
            self.size += 1
        else:
            last = self.dummy_tail.prev
            del self.store[last.key]
            last.val = value
            last.key = key
            self.store[last.key] = last
            self.move_to_head(last)
```
