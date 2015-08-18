title: Leetcode解题-去除有序数组中的重复元素II
date: 2015-08-18 17:28:17
tags: [Leetcode, Coding, Array]
categories: [编程题]
---

## 描述

> Follow up for "Remove Duplicates":
> What if duplicates are allowed at most twice?
>
> For example,
> Given sorted array nums = [1,1,1,2,2,3],
>
> Your function should return length = 5, with the first five elements of nums being 1, 1, 2, 2 and 3. It doesn't matter what you leave beyond the new length.

基本设定和[上一题][1]是一样的，但是难度稍有增加，允许同一元素出现至多两次，比如[1, 1, 1, 2, 2, 3]中1出现了3次，去重后保留2次，2出现2次，全保留，3出现1次，全保留。去重后原数组变为[1, 1, 2, 2, 3]，长度为5。

## 分析

由于相同元素肯定“扎堆出现”，修改[上一题][1]的代码，只要添加一个计数器，记录当前元素已经出现的个数就可以。时间复杂度O(n)，空间复杂度O(1)。


## 代码

### Python
```python
class Solution:
    def removeDuplicates(self, nums):
        if not nums:
            return 0
        m = 1  # counter
        i = 1
        for n in nums[1:]:
            if m < 2 or n != nums[i - 1]:
                nums[i] = n
                m = 1 if n != nums[i - 1] else m + 1  # reset m -> 1 if a new number occurs
                i += 1
        return i
```

[1]: /2015/08/18/remove-duplicates-from-sorted-array/
