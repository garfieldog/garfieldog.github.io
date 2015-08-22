title: Leetcode解题-Permutation Sequence
date: 2015-08-22 15:33:28
tags: [Leetcode, Array, Permutation, 康托展开]
categories: [编程题]
---

## 描述
> The set [1,2,3,…,n] contains a total of n! unique permutations.
>
> By listing and labeling all of the permutations in order,
> We get the following sequence (ie, for n = 3):
>
> "123"
> "132"
> "213"
> "231"
> "312"
> "321"
> Given n and k, return the kth permutation sequence.
>
> Note: Given n will be between 1 and 9 inclusive.

## 分析

我们在上一题[Next Permutation][1]得出了给定一个排列求下一个排列的解法。那对于这道题，最直接的办法，就是从第一个排列开始，调用`k - 1`次`next permutation`嘛，这样的解法时间复杂度是`O(n^2)`。但这样显然有许多浪费，我们只要`第k个`，而不需要`前k个`，有没有更快的方法呢？

### 康托展开

[康托展开][2]是一个全排列到一个自然数的双射，给定一个排列，可以计算出它在所有由小到大全排列中的顺序，并且这个计算是可逆的，这不正是我们要的么？康托展开的公式是
$$ X = a\_n(n-1)! + a\_{n-1}(n-2)! + ... + a\_1 \cdot 0! $$
维基百科[康托展开][2]条目下的例子很好，我们直接拿来用：

> 例如，3 5 7 4 1 2 9 6 8 展开为 98884。因为`X=2*8!+3*7!+4*6!+2*5!+0*4!+0*3!+2*2!+0*1!+0*0!=98884`.
> 解释：
> 排列的第一位是3，比3小的数有两个，以这样的数开始的排列有8!个，因此第一项为`2*8!`
> 排列的第二位是5，比5小的数有1、2、3、4，由于3已经出现，因此共有3个比5小的数，这样的排列有7!个，因此第二项为`3*7!`
> 以此类推，直至`0*0!`

在这里我们需要的是康托展开的逆运算，就是给定X，求原排列。同样我们引用维基的例子：

> 给定n=5, x=96,
> 首先用96-1得到95，说明x之前有95个排列.(将此数本身减去！)
> 用95去除4! 得到3余23，说明有3个数比第1位小，所以第一位是4.
> 用23去除3! 得到3余5，说明有3个数比第2位小，所以是4，但是4已出现过，因此是5.
> 用5去除2!得到2余1，类似地，这一位是3.
> 用1去除1!得到1余0，这一位是2.
> 最后一位只能是1.
> 所以这个数是45321.


## 代码

### Python
```python
class Solution(object):
    def factorial(self, n):
        x = 1
        for i in range(2, n + 1):
            x *= i
        return x

    def getPermutation(self, n, k):
        """
        :type n: int
        :type k: int
        :rtype: str
        """
        a = k - 1
        seq = range(1, n + 1)
        rs = []
        f = self.factorial(n - 1)
        for i in xrange(n - 1):
            r = seq[a / f]
            seq.remove(r)
            rs.append(r)
            a = a % f
            f /= n - 1 - i
        rs.append(seq[0])
        return ''.join(str(x) for x in rs)

```

[1]: /2015/08/21/next-permutation
[2]: https://zh.wikipedia.org/wiki/%E5%BA%B7%E6%89%98%E5%B1%95%E5%BC%80
