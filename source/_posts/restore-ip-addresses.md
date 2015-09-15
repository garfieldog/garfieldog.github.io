title: Leetcode解题-Restore Ip Addresses
date: 2015-09-15 17:21:25
tags: [Leetcode, 回溯法, DFS]
categories: [编程题]
---

## 描述
> Given a string containing only digits, restore it by returning all possible valid IP address combinations.
>
> For example:
> Given "25525511135",
>
> return ["255.255.11.135", "255.255.111.35"]. (Order does not matter)

## 分析
做了那么多回溯法的题，这道题简直就是套模板。时间`O(n^4)`，空间`O(n)`。

## 代码
### Python
```python
class Solution(object):
    def isValid(self, x):
        if not x or (x[0] == '0' and len(x) > 1) or int(x) > 255:
            return False
        return True

    def dfs(self, s, start, path, rs):
        if len(path) == 4:
            if start == len(s):
                rs.append(path[:])
            return
        for i in xrange(start, len(s)):
            part = s[start:i + 1]
            if not self.isValid(part):
                break
            path.append(part)
            self.dfs(s, i + 1, path, rs)
            path.pop()

    def restoreIpAddresses(self, s):
        """
        :type s: str
        :rtype: List[str]
        """
        if not s:
            return []
        rs = []
        path = []
        self.dfs(s, 0, path, rs)
        return ['.'.join(x) for x in rs]
```
