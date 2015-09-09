title: Leetcode解题-Populating Next Right Pointers in Each Node II
date: 2015-09-09 10:20:45
tags: [Leetcode, Tree, Queue]
categories: [编程题]
---

## 描述
> Follow up for problem "Populating Next Right Pointers in Each Node".
>
> What if the given tree could be any binary tree? Would your previous solution still work?
>
> Note:
>
> You may only use constant extra space.
> For example,
> Given the following binary tree,
>          1
>        /  \
>       2    3
>      / \    \
>     4   5    7
> After calling your function, the tree should look like:
>          1 -> NULL
>        /  \
>       2 -> 3 -> NULL
>      / \    \
>     4-> 5 -> 7 -> NULL

## 分析
我们[上一题][1]的解法直接可以用在这一题上。

## 代码
### Python
```python
from collections import deque


class Solution(object):
    def connect(self, root):
        """
        :type root: TreeLinkNode
        :rtype: nothing
        """
        if not root:
            return
        q = deque()
        q.append(root)
        q.append(None)
        while q:
            cur = q.popleft()
            if cur:
                if q:
                    cur.next = q[0]
                if cur.left:
                    q.append(cur.left)
                if cur.right:
                    q.append(cur.right)
            else:
                if q:
                    q.append(None)  # level end
```

[1]: /2015/09/08/populating-next-right-pointers-in-each-node/
