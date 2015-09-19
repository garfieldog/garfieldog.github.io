title: Leetcode解题-Zigzag Conversion
date: 2015-09-18 19:50:47
tags: [Leetcode, Coding]
categories: [编程题]
---

## 描述
> The string "PAYPALISHIRING" is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)
>
> P   A   H   N
> A P L S I I G
> Y   I   R
> And then read line by line: "PAHNAPLSIIGYIR"
> Write the code that will take a string and make this conversion given a number of rows:
>
> string convert(string text, int nRows);
> convert("PAYPALISHIRING", 3) should return "PAHNAPLSIIGYIR".

## 分析
这道题要找规律，太烦了，直接参考[这里][1]。

## 代码
### Python
```python
class Solution(object):
    def convert(self, s, numRows):
        """
        :type s: str
        :type numRows: int
        :rtype: str
        """
        n = len(s)
        if n <= 1 or numRows == 1:
            return s
        rs = []
        gap = 2 * numRows - 2
        for i in xrange(numRows):
            for j, index in enumerate(xrange(i, n, gap)):
                # index = gap * j + i
                rs.append(s[index])
                # not first row either last row
                if i > 0 and i < numRows - 1:
                    k = index + gap - 2 * i
                    if k < n:
                        rs.append(s[k])
        return ''.join(rs)
```

[1]: http://blog.unieagle.net/2012/11/08/leetcode%E9%A2%98%E7%9B%AE%EF%BC%9Azigzag-conversion/
