title: Leetcode解题-Count and Say
date: 2015-09-06 16:08:10
tags: [Leetcode, String]
categories: [编程题]
---

## 描述
> The count-and-say sequence is the sequence of integers beginning as follows:
> 1, 11, 21, 1211, 111221, ...
>
> 1 is read off as "one 1" or 11.
> 11 is read off as "two 1s" or 21.
> 21 is read off as "one 2, then one 1" or 1211.
> Given an integer n, generate the nth sequence.
>
> Note: The sequence of integers will be represented as a string.

## 分析
暴力法模拟可解，时间复杂度`O(n^2)`，空间`O(n)`，实现不难。更好的方法没有想到。

## 代码
### Python
```python
class Solution(object):
    def countAndSay(self, n):
        """
        :type n: int
        :rtype: str
        """
        s = ['1']
        for i in xrange(n - 1):
            rs = []
            last = None
            count = 0
            for c in s:
                if not last or c == last:
                    last = c
                    count += 1
                else:
                    rs.append(str(count))
                    rs.append(last)
                    last = c
                    count = 1
            rs.append(str(count))
            rs.append(c)
            s = rs
        return ''.join(s)
```
