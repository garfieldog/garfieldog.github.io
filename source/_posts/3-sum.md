title: Leetcode解题-3Sum
date: 2015-08-20 11:24:10
tags: [Leetcode, Array]
categories: [编程题]
---

## 描述
> Given an array S of n integers, are there elements a, b, c in S such that a + b + c = 0? Find all unique triplets in the array which gives the sum of zero.
>
> Note:
> Elements in a triplet (a,b,c) must be in non-descending order. (ie, a ≤ b ≤ c)
> The solution set must not contain duplicate triplets.
> For example, given array S = {-1 0 1 2 -1 -4},
>
> A solution set is:
> (-1, 0, 1)
> (-1, -1, 2)

和上一题[Two Sum][1]有点类似，不过变成了找3个数加和等于给定的数字（这里是0）。需要返回数字本身而不是下标。

## 分析
如果我们固定一个数，那就转换成了[Tow Sum][1]问题，所以，简单的解法就是遍历数组，固定当前数字，然后用[Two Sum][1]的解法，时间和空间复杂度都是`O(n^2)`。

还可以用一种更通用的解法，适用于`k-Sum`问题，排序数组，然后用`k-2`个循环遍历数组，在最内层循环用两个指针左右夹逼找到解。时间复杂度`O(max(nlog(n), n^(k-1))`，空间复杂度`O(1)`。

## 代码

### Python
```python
class Solution:
    # @return a list of lists of length 3, [[val1,val2,val3]]
    def threeSum(self, nums):
        nums.sort()
        rs = set()
        for i in xrange(len(nums) - 2):
            j = i + 1
            k = len(nums) - 1
            while j < k:
                s = nums[i] + nums[j] + nums[k]
                if s == 0:
                    rs.add((nums[i], nums[j], nums[k]))
                    j += 1
                    k -= 1
                elif s > 0:
                    k -= 1
                else:
                    j += 1
        return [list(x) for x in rs]
```


[1]: /2015/08/20/two-sum/
