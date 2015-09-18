title: Leetcode解题-Minimum Window Substring
date: 2015-09-18 14:03:58
tags: [Leetcode, String, 两指针]
categories: [编程题]
---

## 描述
> Given a string S and a string T, find the minimum window in S which will contain all the characters in T in complexity O(n).
>
> For example,
> S = "ADOBECODEBANC"
> T = "ABC"
> Minimum window is "BANC".
>
> Note:
> If there is no such window in S that covers all characters in T, return the emtpy string "".
>
> If there are multiple such windows, you are guaranteed that there will always be only one unique minimum window in S.

## 分析
这道题技巧性很强，题目要求时间`O(n)`。使用两指针`i, j`，j先走，找到第一个满足条件的窗口`[i, j)`，然后让i前进，收缩窗口到尽可能小（同时满足条件），这样就找到了一个候选窗口。然后i向前走一步，破坏了条件，让j重复开始的搜索逻辑。详情参考[这篇文章][1]。

## 代码
### Python
```python
from collections import defaultdict


class Solution(object):
    def minWindow(self, s, t):
        """
        :type s: str
        :type t: str
        :rtype: str
        """
        if not s:
            return ''
        expected = defaultdict(int)
        appeared = defaultdict(int)
        for c in t:
            expected[c] += 1

        i = j = 0
        m = len(t)
        n = len(s)
        min_window = None
        while i < n and j < n:
            while j < n and m > 0:
                if appeared[s[j]] < expected[s[j]]:
                    m -= 1
                appeared[s[j]] += 1
                j += 1

            if m == 0:
                # found a window, minimize it
                while i < n and appeared[s[i]] > expected[s[i]]:
                    appeared[s[i]] -= 1
                    i += 1
                if not min_window or (j - i) < (min_window[1] - min_window[0]):
                    min_window = (i, j)
                # i++
                appeared[s[i]] -= 1
                m += 1
                i += 1
        return min_window and s[min_window[0]: min_window[1]] or ''
```

[1]: http://www.cnblogs.com/TenosDoIt/p/3461301.html
