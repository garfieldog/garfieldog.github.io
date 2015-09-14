title: Leetcode解题-Word Ladder
date: 2015-09-14 15:40:06
tags: [Leetcode, BFS]
categories: [编程题]
---

## 描述
> Given two words (beginWord and endWord), and a dictionary, find the length of shortest transformation sequence from beginWord to endWord, such that:
>
> Only one letter can be changed at a time
> Each intermediate word must exist in the dictionary
> For example,
>
> Given:
> start = "hit"
> end = "cog"
> dict = ["hot","dot","dog","lot","log"]
> As one shortest transformation is "hit" -> "hot" -> "dot" -> "dog" -> "cog",
> return its length 5.
>
> Note:
> Return 0 if there is no such transformation sequence.
> All words have the same length.
> All words contain only lowercase alphabetic characters.

## 分析
寻找最短变换路径，使用广度优先遍历。好好想一想这样找到的路径为什么可以保证是最短的。时间复杂度。

## 代码
### Python
```python
class Solution(object):
    def ladderLength(self, beginWord, endWord, wordDict):
        """
        :type beginWord: str
        :type endWord: str
        :type wordDict: Set[str]
        :rtype: int
        """
        al = 'abcdefghijklmnopqrstuvwxyz'
        q = deque()
        d = 0
        if beginWord:
            q.append(beginWord)
            q.append(None)

        wordDict.add(endWord)
        while q:
            cur = q.popleft()
            if cur:
                if cur == endWord:
                    return d + 1
                arr = list(cur)
                for i in xrange(len(arr)):
                    for c in al:
                        if arr[i] == c:
                            continue
                        tmp = arr[i]
                        arr[i] = c
                        new_word = ''.join(arr)
                        if new_word in wordDict:
                            q.append(new_word)
                            wordDict.remove(new_word)
                        arr[i] = tmp
            else:
                d += 1
                if q:
                    q.append(None)
        return 0
```
