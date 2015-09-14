title: Leetcode解题-Letter Combinations of a Phone Number
date: 2015-09-14 15:17:47
tags: [Leetcode, DFS]
categories: [编程题]
---

## 描述
> Given a digit string, return all possible letter combinations that the number could represent.
>
> A mapping of digit to letters (just like on the telephone buttons) is given below.
> ![phone.png](/images/phone.png)
>
> Input:Digit string "23"
> Output: ["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].
> Note:
> Although the above answer is in lexicographical order, your answer could be in any order you want.

## 分析
依然回溯法。回溯法其实就是n叉树的深度优先遍历。

## 代码
### Python
```python
class Solution(object):
    keyboard = {
        '2': 'abc',
        '3': 'def',
        '4': 'ghi',
        '5': 'jkl',
        '6': 'mno',
        '7': 'pqrs',
        '8': 'tuv',
        '9': 'wxyz'
    }

    def dfs(self, digits, path, rs):
        if len(digits) == len(path):
            rs.append(''.join(path))
            return

        n = len(path)
        for c in self.keyboard.get(digits[n], ''):
            path.append(c)
            self.dfs(digits, path, rs)
            path.pop()

    def letterCombinations(self, digits):
        """
        :type digits: str
        :rtype: List[str]
        """
        if not digits:
            return []
        path = []
        rs = []
        self.dfs(digits, path, rs)
        return rs
```
