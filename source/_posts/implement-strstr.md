title: Leetcode解题-Implement strStr()
date: 2015-08-31 11:50:48
tags: [Leetcode, String, KMP, BM]
categories: [编程题]
---

## 描述
> Implement strStr().
>
> Returns the index of the first occurrence of needle in haystack, or -1 if needle is not part of haystack.

## 分析
查找子字符串，暴力搜索时间复杂度`O(mn)`，其中`m``n`分别是haystack和need的长度。还有很多经典算法，如[KMP][1]，[Boyer-Moore][3]。KMP算法最坏是时间`O(m + n)`的，实现可以参考[Wiki][1]或[KMP算法详解][2]。[Boyer-Moore][3]算法实际情况下表现通常优于KMP，尽管它（needle在haystack中时的）最坏情况下时间是`O(mn)`的。可以参考[字符串匹配的Boyer-Moore算法][4]。

因为`BM`算法使用了两个启发式规则（`坏字符`和`好后缀`）来移动needle，而这两个规则是独立的，所以其实用一个也不影响正确性，实现起来方便，只是运行稍慢一些。

## 代码

### 暴力搜索
```python
class Solution(object):
    def match(self, haystack, i, needle):
        for k in xrange(len(needle)):
            if haystack[i + k] != needle[k]:
                return False
        return True

    def strStr(self, haystack, needle):
        """
        :type haystack: str
        :type needle: str
        :rtype: int
        """
        m, n = len(haystack), len(needle)
        for i in xrange(m - n + 1):
            if self.match(haystack, i, needle):
                return i
        return -1
```

### KMP
```python
class Solution(object):
    def strStr(self, haystack, needle):
        """
        :type haystack: str
        :type needle: str
        :rtype: int
        """
        if not needle:
            return 0
        m, n = len(haystack), len(needle)

        # pre-calculate `p` array
        p = [0]
        j = 0
        for i in xrange(1, n):
            while j > 0 and needle[i] != needle[j]:
                j = p[j - 1]
            if needle[i] == needle[j]:
                j = j + 1
            p.append(j)

        j = 0
        for i in xrange(m):
            while j > 0 and haystack[i] != needle[j]:
                j = p[j - 1]
            if haystack[i] == needle[j]:
                j += 1
            if j == n:
                return i - n + 1
        return -1
```

### 简化版BM（只有坏字符，没有好前缀）
```python
class Solution(object):
    def strStr(self, haystack, needle):
        """
        :type haystack: str
        :type needle: str
        :rtype: int
        """
        if not needle:
            return 0
        m, n = len(haystack), len(needle)
        p = {x: i for i, x in enumerate(needle)}
        i = n - 1
        while i < m:
            found = True
            for j in xrange(n):
                if haystack[i - j] != needle[n - 1 - j]:
                    c = p.get(haystack[i - j], -1)
                    new_i = i - j + n - 1 - c
                    if new_i <= i:
                        i += 1
                    else:
                        i = new_i
                    found = False
                    break
            if found:
                return i - n + 1
        return -1
```

### 完整BM
TBD

[1]: https://en.wikipedia.org/wiki/Knuth%E2%80%93Morris%E2%80%93Pratt_algorithm
[2]: http://www.matrix67.com/blog/archives/115
[3]: https://en.wikipedia.org/wiki/Boyer%E2%80%93Moore_string_search_algorithm
[4]: http://www.ruanyifeng.com/blog/2013/05/boyer-moore_string_search_algorithm.html
