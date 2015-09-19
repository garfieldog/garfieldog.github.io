title: Leetcode解题-Text Justification
date: 2015-09-19 11:03:41
tags: [Leetcode, Coding]
categories: [编程题]
---

## 描述
> Given an array of words and a length L, format the text such that each line has exactly L characters and is fully (left and right) justified.
>
> You should pack your words in a greedy approach; that is, pack as many words as you can in each line. Pad extra spaces ' ' when necessary so that each line has exactly L characters.
>
> Extra spaces between words should be distributed as evenly as possible. If the number of spaces on a line do not divide evenly between words, the empty slots on the left will be assigned more spaces than the slots on the right.
>
> For the last line of text, it should be left justified and no extra space is inserted between words.
>
> For example,
> words: ["This", "is", "an", "example", "of", "text", "justification."]
> L: 16.
>
> Return the formatted lines as:
> [
>    "This    is    an",
>    "example  of text",
>    "justification.  "
> ]
> Note: Each word is guaranteed not to exceed L in length.
>
> Corner Cases:
> A line other than the last line might contain only one word. What should you do in this case?
> In this case, that line should be left-justified.

## 分析
细节实现题，给文章排版，要求每一行左右对齐（最后一行左对齐）。主要是要注意各种特殊情况，尤其是一行只有一个单词的情况。

## 代码
### Python
```python
class Solution(object):
    def fullJustify(self, words, maxWidth):
        """
        :type words: List[str]
        :type maxWidth: int
        :rtype: List[str]
        """
        rs = []
        curLineWidth = 0
        line = []
        for w in words:
            if curLineWidth + len(line) + len(w) <= maxWidth:
                line.append(w)
                curLineWidth += len(w)
            else:
                spaces = maxWidth - curLineWidth
                if len(line) == 1:
                    s = line[0] + ' ' * spaces
                else:
                    a, b = divmod(spaces, len(line) - 1)
                    buff = []
                    for i in xrange(len(line)):
                        buff.append(line[i])
                        if i < b:
                            buff.append(' ' * (a + 1))
                        elif i < len(line) - 1:
                            buff.append(' ' * a)
                    s = ''.join(buff)
                rs.append(s)
                line = [w]
                curLineWidth = len(w)
        if line:
            s = ' '.join(line) + ' ' * (maxWidth - curLineWidth - len(line) + 1)
            rs.append(s)

        return rs
```
