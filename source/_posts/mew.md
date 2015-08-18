title: Mew
date: 2015-08-18 10:56:14
categories: [Mew]
---

## 猪肉卷

> 我见过你们人类难以置信的事，
> 我见过太空飞船在猎户星座的边缘被击中，
> 燃起熊熊火光。
> 我见过Ｃ射线，
> 划过“唐怀瑟之门”那幽暗的宇宙空间。
> 然而所有的这些时刻都将消失在时间里，
> 就像……泪水……消失在雨中一样。
> ……
> 哎这炸酱面该下锅了吧！？

## 千层面

$ E = mc^2 $


## 披萨

``` python
def partition(arr, start, end):
    pivot = arr[start]
    arr[end], arr[start] = arr[start], arr[end]
    i = start
    for j in xrange(start, end, 1):
        if arr[j] <= pivot:
            if i != j:
                arr[i], arr[j] = arr[j], arr[i]
            i += 1
    arr[end], arr[i] = arr[i], arr[end]
    return i


def qsort_r(arr, start, end):
    if start < end:
        p = partition(arr, start, end)
        qsort_r(arr, start, p - 1)
        qsort_r(arr, p + 1, end)


def qsort(arr):
    qsort_r(arr, 0, len(arr) - 1)
```
