title: Leetcode解题-Valid Sudoku
date: 2015-08-22 16:50:10
tags: [Leetcode, 数独, 矩阵]
categories: [编程题]
---

## 描述

> Determine if a Sudoku is valid, according to: [Sudoku Puzzles - The Rules][1].
>
> The Sudoku board could be partially filled, where empty cells are filled with the character '.'.
>
> ![sudoku.png](/images/sudoku.png)
>
> A partially filled sudoku which is valid.
>
> Note:
> A valid Sudoku board (partially filled) is not necessarily solvable. Only the filled cells need to be validated.

判断一个数独棋盘状态是不是合法（不需要可解）。

## 分析

可以分三次遍历棋盘，分别检查行、列、和小九宫格是否合法(同一数字最多出现一次)。时间复杂度`O(n^2)`，空间复杂度`O(n)`。还可以把三次遍历合并为一次，空间复杂度增加至`O(n^2)`，时间复杂度系数项减小。

## 代码

### Python
```python
class Solution(object):
    def isValidSudoku(self, board):
        """
        :type board: List[List[str]]
        :rtype: bool
        """
        n = len(board)
        used_cols = [[False] * n for i in xrange(n)]
        used_cells = [[False] * n for i in xrange(n)]
        for i in xrange(n):
            used_row = [False] * n
            for j in xrange(n):
                if board[i][j] != '.':
                    k = int(board[i][j]) - 1
                    if not self.check(used_row, k) or \
                       not self.check(used_cols[j], k) or \
                       not self.check(used_cells[j / 3 * 3 + i / 3], k):
                            return False
        return True

    def check(self, flags, k):
        valid = not flags[k]
        if not flags[k]:
            flags[k] = True
        return valid
```


[1]: http://sudoku.com.au/TheRules.aspx
