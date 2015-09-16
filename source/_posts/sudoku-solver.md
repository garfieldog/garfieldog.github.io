title: Leetcode解题-Sudoku Solver
date: 2015-09-16 10:03:58
tags: [Leetcode, 回溯法, Sudoku]
categories: [编程题]
---

## 描述
> Write a program to solve a Sudoku puzzle by filling the empty cells.
>
> Empty cells are indicated by the character '.'.
>
> You may assume that there will be only one unique solution.
>
> ![puzzle](/images/sudoku1.png)
>
> ![solver](/images/sudoku2.png)

## 分析
这道题是有一定难度的，虽然也是回溯法，但和我们之前熟悉的模式不同，不具备使用dfs的条件，因为『待填充』的位置之间不具备联通关系，使用一个三重循环来回溯。时间复杂度`O(n^4)`，如果使用三个哈希表来保存对应位置`行、列、九宫格`可用的数字，时间复杂度可降到`O(n^3)`，空间`O(n^2)`。

## 代码
### Python
```python
from collections import defaultdict


class Solution(object):

    def solveSudoku(self, board):
        """
        :type board: List[List[str]]
        :rtype: void Do not return anything, modify board in-place instead.
        """
        def solve():
            for x in xrange(9):
                for y in xrange(9):
                    if board[x][y] == '.':
                        z = x / 3 * 3 + y / 3
                        available = row[x] & col[y] & grid[z]
                        for i in available:
                            board[x][y] = i
                            row[x].remove(i)
                            col[y].remove(i)
                            grid[z].remove(i)
                            if solve():
                                return True
                            board[x][y] = '.'
                            row[x].add(i)
                            col[y].add(i)
                            grid[z].add(i)
                        return False
            return True

        row = defaultdict(lambda: set(str(x) for x in xrange(1, 10)))
        col = defaultdict(lambda: set(str(x) for x in xrange(1, 10)))
        grid = defaultdict(lambda: set(str(x) for x in xrange(1, 10)))
        for x in xrange(9):
            for y in xrange(9):
                if board[x][y] != '.':
                    z = x / 3 * 3 + y / 3
                    row[x].remove(board[x][y])
                    col[y].remove(board[x][y])
                    grid[z].remove(board[x][y])
        solve()
```
