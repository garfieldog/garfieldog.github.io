title: Leetcode解题-Simplify Path
date: 2015-09-06 17:25:02
tags: [Leetcode, String, Stack]
categories: [编程题]
---

## 描述
> Given an absolute path for a file (Unix-style), simplify it.
>
> For example,
> path = "/home/", => "/home"
> path = "/a/./b/../../c/", => "/c"
>
> Corner Cases:
> Did you consider the case where path = "/../"?
> In this case, you should return "/".
> Another corner case is the path might contain multiple slashes '/' together, such as "/home//foo/".
> In this case, you should ignore redundant slashes and return "/home/foo".

## 分析
比较简单，用stack，注意corner cases。时间`O(n)`，空间`O(n)`。

## 代码
### Python
```python
class Solution(object):
    def simplifyPath(self, path):
        """
        :type path: str
        :rtype: str
        """
        ps = path.split('/')
        ss = []
        for p in ps:
            if p == '.' or p == '':
                continue
            elif p == '..':
                if len(ss) > 0:
                    ss.pop()
            else:
                ss.append(p)
        return '/' + '/'.join(ss)
```
