title: Leetcode解题-Single Number III
date: 2015-08-25 13:46:34
tags: [Leetcode, Array, 位运算]
categories: [编程题]
---

## 描述

> Given an array of numbers nums, in which exactly two elements appear only once and all the other elements appear exactly twice. Find the two elements that appear only once.
>
> For example:
>
> Given nums = [1, 2, 1, 3, 2, 5], return [3, 5].
>
> Note:
> The order of the result is not important. So in the above example, [5, 3] is also correct.
> Your algorithm should run in linear runtime complexity. Could you implement it using only constant space complexity?

## 分析
和[Single Number][1]基本设定一致，区别在于这次有两个出现一次的数，设为`x`和`y`。这给我们了一点启发，那我们是不是可以套用[Single Number]的解法呢？是可以的，不过我们给所有数取异或后，剩下的值是 $ z = x \oplus y
$，这时候我们要怎么把x和y给分别求出来呢？我们只需要用一个bit位就能够区分出来，任取z的为1的某一位（说明x和y在这一位上不一致），把原数组中这一位是1的数放到一拨，为0的放到一拨，分别取异或，就解出了x和y。

取z的某一位为1的bit位，可以就用[LSB][2]，它有一个漂亮的求法`n & -n`，更多位运算的奇技淫巧看这里：[Bit Twiddling Hacks][3]。

## 代码

### Python
```
class Solution(object):
    def singleNumber(self, nums):
        """
        :type nums: List[int]
        :rtype: List[int]
        """
        z = reduce(lambda x, y: x ^ y, nums)
        lsb = z & -z
        x, y = 0, 0
        for n in nums:
            if n & lsb:
                x ^= n
            else:
                y ^= n
        return [x, y]
```

[1]: /2015/08/25/single-number/
[2]: https://zh.wikipedia.org/wiki/%E6%9C%80%E4%BD%8E%E6%9C%89%E6%95%88%E4%BD%8D
[3]: https://graphics.stanford.edu/~seander/bithacks.html
