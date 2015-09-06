title: Leetcode解题-Group Anagrams
date: 2015-09-06 16:30:58
tags: [Leetcode, String, 哈希表]
categories: [编程题]
---

## 描述
> Given an array of strings, group anagrams together.
>
> For example, given: ["eat", "tea", "tan", "ate", "nat", "bat"], 
> Return:
>
> [
>   ["ate", "eat","tea"],
>   ["nat","tan"],
>   ["bat"]
> ]
> Note:
> For the return value, each inner list's elements must follow the lexicographic order.
> All inputs will be in lower-case.

## 分析
用哈希表，理论上可以时间`O(nlogn)`，空间`O(n)`。我们下面的实现由于用了数组而不是链表，所以要慢一些，最坏情况`O(n^2)`。

## 代码
### Python
```python
from bisect import bisect


class Solution(object):
    def groupAnagrams(self, strs):
        """
        :type strs: List[str]
        :rtype: List[List[str]]
        """
        d = {}
        for s in strs:
            key = ''.join(sorted(s))
            d.setdefault(key, [])
            rs = d[key]
            idx = bisect(rs, s)
            rs.insert(idx, s)
        return d.values()
```
