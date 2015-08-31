title: Leetcode解题-Add Binary
date: 2015-08-31 18:47:58
tags: [Leetcode, String]
categories: [编程题]
---

## 描述
> Given two binary strings, return their sum (also a binary string).
>
> For example,
> a = "11"
> b = "1"
> Return "100".

## 分析
简单题。

## 代码

### Python
```python
class Solution(object):
    def addBit(self, a, b, c):
        s = int(a) + int(b) + int(c)
        return divmod(s, 2)

    def reverse(self, arr):
        n = len(arr)
        for i in xrange(n / 2):
            arr[i], arr[n - 1 - i] = arr[n - 1 - i], arr[i]

    def addBinary(self, a, b):
        """
        :type a: str
        :type b: str
        :rtype: str
        """
        m, n = len(a), len(b)
        if m > n:
            return self.addBinary(b, a)

        rs = []
        c = 0
        for i in xrange(m):
            c, x = self.addBit(a[m - 1 - i], b[n - 1 - i], c)
            rs.append(str(x))

        for i in xrange(m, n):
            c, x = self.addBit(b[n - 1 - i], 0, c)
            rs.append(str(x))

        if c == 1:
            rs.append('1')
        self.reverse(rs)
        return ''.join(rs)
```
