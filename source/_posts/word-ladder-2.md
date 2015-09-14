title: Leetcode解题-Word Ladder II
date: 2015-09-14 16:18:05
tags: [Leetcode, BFS]
categories: [编程题]
---

## 描述
> Given two words (start and end), and a dictionary's word list, find all shortest transformation sequence(s) from start to end, such that:
>
> Only one letter can be changed at a time
> Each intermediate word must exist in the word list
> For example,

> Given:
> start = "hit"
> end = "cog"
> wordList = ["hot","dot","dog","lot","log"]
> Return
>   [
>     ["hit","hot","dot","dog","cog"],
>     ["hit","hot","lot","log","cog"]
>   ]
> Note:
> All words have the same length.
> All words contain only lowercase alphabetic characters.

## 分析
这道题比较难，要把所有的最短路径都找出来。其实本质上就是标准的求的图两点间最小路径。先BFS遍历记录路径信息，再DFS反向构建路径。

难点在于第一要维护路径的信息，第二不能像上一题那样直接从字典中删掉入列的词（因为它可能存在于两条最短路径上）。写了很久没有写对，先放一个[别人的正确答案][1]，解法很漂亮，回头详细分析。

## 代码
### Python
```python
from collections import defaultdict
import string


class Solution:
    def findLadders(self, start, end, wordlist):
        """
        :type start: str
        :type end: str
        :type wordlist: Set[str]
        :rtype: List[List[int]]
        """
        wordlist.add(end)
        level = {start}
        parents = defaultdict(set)  # pre-node in shortest paths
        while level and end not in parents:
            next_level = defaultdict(set)
            for node in level:
                for char in string.ascii_lowercase:
                    for i in range(len(start)):
                        n = node[:i] + char + node[i + 1:]
                        if n in wordlist and n not in parents:
                            next_level[n].add(node)
            level = next_level  # actually it means `level = next_level.keys()`
            parents.update(next_level)
        res = [[end]]
        while res and res[0][0] != start:
            res = [[p] + r for r in res for p in parents[r[0]]]
        return res
```

[1]: https://leetcode.com/discuss/24191/defaultdict-for-traceback-and-easy-writing-lines-python-code
