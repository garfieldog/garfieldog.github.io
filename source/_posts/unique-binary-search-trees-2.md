title: Leetcode解题-Unique Binary Search Trees II
date: 2015-09-09 13:58:37
tags: [Leetcode, Tree, 动态规划]
categories: [编程题]
---

## 描述
> Given n, generate all structurally unique BST's (binary search trees) that store values 1...n.
>
> For example,
> Given n = 3, your program should return all 5 unique BST's shown below.
>
>    1         3     3      2      1
>     \       /     /      / \      \
>      3     2     1      1   3      2
>     /     /       \                 \
>    2     1         2                 3

## 分析
[上一题][1]只需要数数，这一题要求把所有的树都构建出来。思路一样，用递归更直观一些。

## 代码
### Python
```python
class Solution(object):
    def generateTreesR(self, start, end):
        if start > end:
            return [None]

        rs = []
        for i in xrange(start, end + 1):
            lefts = self.generateTreesR(start, i - 1)
            rights = self.generateTreesR(i + 1, end)
            for left in lefts:
                for right in rights:
                    node = TreeNode(i)
                    node.left = left
                    node.right = right
                    rs.append(node)
        return rs

    def generateTrees(self, n):
        """
        :type n: int
        :rtype: List[TreeNode]
        """
        return self.generateTreesR(1, n)
```

[1]: /2015/09/09/unique-binary-search-trees/
