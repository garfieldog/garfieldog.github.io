title: Leetcode解题-Multiply Strings
date: 2015-09-18 15:30:54
tags: [Leetcode, String]
categories: [编程题]
---

## 描述
> Given two numbers represented as strings, return multiplication of the numbers as a string.
>
> Note: The numbers can be arbitrarily large and are non-negative.

## 分析
大整数乘法，把字符串转换为数组，然后数组相乘。我们这里用9个字符组成一个数字，可以任意选 `0 < n < 10`的长度。(10位以上的字符串不能用一个32位整数存储)

## 代码
### Python
```python
UNIT_LEN = 9
BASE = 1000000000


class Solution(object):
    def str2vec(self, s):
        n = len(s)
        v = []
        for end in xrange(n, 0, -UNIT_LEN):
            start = max(end - UNIT_LEN, 0)
            v.append(int(s[start: end]))
        return v

    def vec2str(self, vec):
        fmt = '%%0%dd' % UNIT_LEN
        ss = [str(vec[len(vec) - 1])]
        for i in xrange(len(vec) - 2, -1, -1):
            ss.append(fmt % vec[i])
        return ''.join(ss)

    def multiply_vec(self, v1, v2):
        n1 = len(v1)
        n2 = len(v2)
        v = [0] * (n1 + n2)
        for i in xrange(n1):
            for j in xrange(n2):
                v[i + j] += v1[i] * v2[j]
                if v[i + j] >= BASE:
                    v[i + j + 1] += v[i + j] / BASE
                    v[i + j] %= BASE
        while len(v) > 1 and v[-1] == 0:
            v.pop()
        return v

    def multiply(self, num1, num2):
        """
        :type num1: str
        :type num2: str
        :rtype: str
        """
        if not num1 or not num2:
            return ''
        vec1 = self.str2vec(num1)
        vec2 = self.str2vec(num2)
        v = self.multiply_vec(vec1, vec2)
        return self.vec2str(v)
```
