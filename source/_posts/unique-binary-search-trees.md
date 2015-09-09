title: Leetcode解题-Unique Binary Search Trees
date: 2015-09-09 13:35:38
tags: [Leetcode, Tree, 动态规划]
categories: [编程题]
---

## 描述
> Given n, how many structurally unique BST's (binary search trees) that store values 1...n?
>
> For example,
> Given n = 3, there are a total of 5 unique BST's.
>
>    1         3     3      2      1
>     \       /     /      / \      \
>      3     2     1      1   3      2
>     /     /       \                 \
>    2     1         2                 3

## 分析
因为是搜索二叉树，所以一旦选定根节点，那么左子树和右子树含有哪些元素就确定了，那么显然可以变成一个递归的问题。以选定节点为根的搜索二叉树有`左子树可能的个数 * 右子树可能的个数`。所以给定总元素数`n`，不同的搜索二叉树个数`f(n)`就有：

$$ f(n) = \sum\_{i=0}^{n - 1} f(i)\*f(n - 1 - i) $$

用动态规划解，时间`O(n^2)`，空间`O(n)`。

## 代码
### Python
```python
class Solution(object):
    def numTrees(self, n):
        """
        :type n: int
        :rtype: int
        """
        arr = [0] * (n + 1)
        arr[0] = arr[1] = 1
        for i in xrange(2, n + 1):
            for j in xrange(i):
                arr[i] += arr[j] * arr[i - 1 - j]
        return arr[n]
```
