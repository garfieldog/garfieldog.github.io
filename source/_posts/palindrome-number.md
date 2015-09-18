title: Leetcode解题-Palindrome Number
date: 2015-09-18 11:11:03
tags: [Leetcode, Coding, Palindrome]
categories: [编程题]
---

## 描述
> Determine whether an integer is a palindrome. Do this without extra space.
>
> Some hints:
> Could negative integers be palindromes? (ie, -1)
>
> If you are thinking of converting the integer to string, note the restriction of using extra space.
>
> You could also try reversing an integer. However, if you have solved the problem "Reverse Integer", you know that the reversed integer might overflow. How would you handle such case?
>
> There is a more generic way of solving this problem.

## 分析
用[Reverse Integer][1]中实现的方法，把整数翻转看结果是否和它自己相等（另外注意负数不可能是回文）。还有一种解法，就是和[字符串判别回文][2]差不多，两指针从两边夹逼。

## 代码
### 翻转整数
```python
class Solution(object):
    def reverse(self, x):
        sign = 1 if x >= 0 else -1
        x = abs(x)
        r = 0
        while x:
            x, mod = divmod(x, 10)
            r = r * 10 + mod
            # overflow check
            if r > 2147483647:
                return 0
        return sign * r

    def isPalindrome(self, x):
        """
        :type x: int
        :rtype: bool
        """
        if x < 0:
            return False
        return self.reverse(x) == x
```

### 头尾遍历
```python
class Solution(object):
    def isPalindrome(self, x):
        """
        :type x: int
        :rtype: bool
        """
        if x < 0:
            return False
        divisor = 1
        while divisor * 10 < x:
            divisor *= 10
        while x >= 10:
            head, x = divmod(x, divisor)
            x, tail = divmod(x, 10)
            if head != tail:
                return False
            divisor /= 100
        return True
```

[1]: /2015/09/18/reverse-integer/
[2]: /2015/08/31/valid-palindrome/
