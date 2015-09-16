title: Leetcode解题-Word Search
date: 2015-09-16 11:34:04
tags: [Leetcode, 回溯法]
categories: [编程题]
---

## 描述
> Given a 2D board and a word, find if the word exists in the grid.
>
> The word can be constructed from letters of sequentially adjacent cell, where "adjacent" cells are those horizontally or vertically neighboring. The same letter cell may not be used more than once.
>
> For example,
> Given board =
>
> [
>   ["ABCE"],
>   ["SFCS"],
>   ["ADEE"]
> ]
> word = "ABCCED", -> returns true,
> word = "SEE", -> returns true,
> word = "ABCB", -> returns false.

## 分析
回溯+DFS，一开始的思路是先找到第一个字符，然后在上面开始深搜，结果一直有bug，在一些corner case上会陷入死循环。回到最简单的方式，在所有格子上深搜。

## 代码
### DFS + 回溯
```python
class Solution(object):
    def dfs(self, board, word, start, x, y, used):
        if start == len(word):
            return True
        m = len(board)
        n = len(board[0])
        if x < 0 or y < 0 or x >= m or y >= n or board[x][y] != word[start] or used[x][y]:
            return False
        used[x][y] = True
        candidates = [(x - 1, y), (x + 1, y), (x, y - 1), (x, y + 1)]
        for i, j in candidates:
            if self.dfs(board, word, start + 1, i, j, used):
                return True
        used[x][y] = False
        return False

    def exist(self, board, word):
        """
        :type board: List[List[str]]
        :type word: str
        :rtype: bool
        """
        m = len(board)
        if m == 0:
            return False
        n = len(board[0])
        if n == 0:
            return False
        if len(word) == 0:
            return False
        used = [[False] * n for i in xrange(m)]
        for i in xrange(m):
            for j in xrange(n):
                if self.dfs(board, word, 0, i, j, used):
                    return True
        return False
```
