title: Leetcode解题-Gary Code
date: 2015-08-24 14:29:49
tags: [Leetcode, 格雷码, 数学, 递归]
categories: [编程题]
---

## 描述

> The gray code is a binary numeral system where two successive values differ in only one bit.
>
> Given a non-negative integer n representing the total number of bits in the code, print the sequence of gray code. A gray code sequence must begin with 0.
>
> For example, given n = 2, return [0,1,3,2]. Its gray code sequence is:
>
> 00 - 0
> 01 - 1
> 11 - 3
> 10 - 2
> Note:
> For a given n, a gray code sequence is not uniquely defined.
>
> For example, [0,2,3,1] is also a valid gray code sequence according to the above definition.
>
> For now, the judge is able to judge based on one instance of gray code sequence. Sorry about that.

## 分析

格雷码有数学公式：第n个格雷码`G(n)= n xor (n / 2)`，因此只要顺序给出从0到`2^n -1`个格雷码就可以。

数学公式虽然精妙，但如果你不知道这个公式，是很难现场推出来的。还可以从定义出发，递归给出格雷码:

1. 当n=1时，格雷码序列是`L(1) = [0, 1]`
2. 当n>1时，格雷码序列是 `0前缀 ++ L(n - 1)` 和`1前缀 ++ reverse(L(n - 1))`的拼接。


## 代码

### 公式法
```python
class Solution(object):
    def grayCode(self, n):
        """
        :type n: int
        :rtype: List[int]
        """
        rs = []
        for i in xrange(2 ** n):
            rs.append(i ^ (i / 2))
        return rs
```

### 递归法
```python
class Solution(object):
    def grayCode(self, n):
        """
        :type n: int
        :rtype: List[int]
        """
        rs = [0]
        for i in xrange(n):
            h = 1 << i
            for j in xrange(len(rs) - 1, -1, -1):
                rs.append(h | rs[j])
        return rs
```
