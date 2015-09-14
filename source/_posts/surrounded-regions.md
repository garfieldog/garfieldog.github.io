title: Leetcode解题-Surrounded Regions
date: 2015-09-14 19:11:24
tags: [Leetcode, BFS]
categories: [编程题]
---

## 描述
> Given a 2D board containing 'X' and 'O', capture all regions surrounded by 'X'.
>
> A region is captured by flipping all 'O's into 'X's in that surrounded region.
>
> For example,
> X X X X
> X O O X
> X X O X
> X O X X
> After running your function, the board should be:
>
> X X X X
> X X X X
> X X X X
> X O X X

## 分析
有点像苹果棋的规则。如果一个`O`能够沿着`O`构成的路径通往边界，它就是安全的（不会被`X`掉）。我们从边缘四周的`O`开始做深度或广度优先遍历，把安全的`O`都标记起来。

## 代码
### BFS（会超时）
```python
from collections import deque


class Solution(object):
    def bfs(self, board, i, j):
        def is_valid(x, y):
            if x < 0 or y < 0 or x >= m or y >= n or board[x][y] != 'O':
                return False
            return True

        m = len(board)
        n = len(board[0])
        q = deque()
        if is_valid(i, j):
            q.append((i, j))
        while q:
            x, y = q.popleft()
            board[x][y] = '*'
            for i, j in [(x - 1, y), (x + 1, y), (x, y - 1), (x, y + 1)]:
                if is_valid(i, j):
                    q.append((i, j))

    def solve(self, board):
        """
        :type board: List[List[str]]
        :rtype: void Do not return anything, modify board in-place instead.
        """
        m = len(board)
        if m == 0:
            return
        n = len(board[0])
        if n == 0:
            return
        for i in xrange(m):
            self.bfs(board, i, 0)
            self.bfs(board, i, n - 1)
        for j in xrange(n):
            self.bfs(board, 0, j)
            self.bfs(board, m - 1, j)

        for i in xrange(m):
            for j in xrange(n):
                if board[i][j] == 'O':
                    board[i][j] = 'X'
                elif board[i][j] == '*':
                    board[i][j] = 'O'
```

### 优化后的BFS
```python
from collections import deque


class Solution(object):
    def solve(self, board):
        """
        :type board: List[List[str]]
        :rtype: void Do not return anything, modify board in-place instead.
        """
        def is_valid(x, y):
            if x < 0 or y < 0 or x >= m or y >= n or board[x][y] != 'O' or visited[x][y]:
                return False
            return True

        m = len(board)
        if m == 0:
            return
        n = len(board[0])
        if n == 0:
            return

        visited = [[False] * n for i in xrange(m)]
        q = deque()
        for i in xrange(m):
            if is_valid(i, 0):
                q.append((i, 0))
            if is_valid(i, n - 1):
                q.append((i, n - 1))
        for j in xrange(n):
            if is_valid(0, j):
                q.append((0, j))
            if is_valid(m - 1, j):
                q.append((m - 1, j))

        while q:
            x, y = q.popleft()
            board[x][y] = '*'
            visited[x][y] = True
            for i, j in [(x - 1, y), (x + 1, y), (x, y - 1), (x, y + 1)]:
                if is_valid(i, j):
                    q.append((i, j))

        for i in xrange(m):
            for j in xrange(n):
                if board[i][j] == 'O':
                    board[i][j] = 'X'
                elif board[i][j] == '*':
                    board[i][j] = 'O'
```
