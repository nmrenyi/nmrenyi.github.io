---
layout:     post
title:      BinarySearch
subtitle:   Brief summary on binary search.
date:       2020-07-02
author:     RenYi
# header-img: img/post-bg-cook.jpg
catalog: true
tags:
    - Data Structure and Algorithm
---

## Scenario Description

We have a sorted array `a[n]` here. Given a target value, we need to search for it in O(logn) time. 
If the target value is in `a[n]`, return its index. Otherwise return the last index of the largest value that is smaller than the target value.



## Solution

Here we use binary search, which select the middle element and compare it with the target value, which may decrease the problem size by half.

Let's see the code first, reference to Junhui Deng at DSA class in Tsinghua.

```C++
/******************************************************************************************
 * Data Structures in C++
 * ISBN: 7-302-33064-6 & 7-302-33065-3 & 7-302-29652-2 & 7-302-26883-3
 * Junhui DENG, deng@tsinghua.edu.cn
 * Computer Science & Technology, Tsinghua University
 * Copyright (c) 2003-2019. All rights reserved.
 ******************************************************************************************/

// 二分查找算法（版本C）：在有序向量的区间[lo, hi)内查找元素e，0 <= lo <= hi <= _size
template <typename T> static Rank binSearch ( T* S, T const& e, Rank lo, Rank hi ) {
   while ( lo < hi ) {  // 每步迭代仅需做一次比较判断，有两个分支
      Rank mi = ( lo + hi ) >> 1;  //以中点为轴点（区间宽度的折半，等效于宽度之数值表示的右移）
      ( e < S[mi] ) ? hi = mi : lo = mi + 1;  //经比较后确定深入[lo, mi)或(mi, hi)
   }  // 成功查找不能提前终止
   return lo - 1; // 循环结束时，lo为大于e的元素的最小秩，故lo - 1即不大于e的元素的最大秩
}  // 有多个命中元素时，总能保证返回秩最大者；查找失败时，能够返回失败的位置
```

In this code, `S[lo - 1]` is always is element that can be determined to be the largest value that is no larger than the target element. And `S[hi]` is always the smallest element larger than the target element which can be determined now. And when the loop breaks out, we have `lo == hi`, which means the non-determined interval's length is zero now, and `S[lo - 1]` is the element no larger than the target value with the largest index. So we return `lo - 1` in the end.

As for how the algorithm returns the largest value for the elements with the same value as the target, I think it works because `lo = mi + 1` when `e == S[mi]`, and `S[hi]` is always bigger than `e`. Then whenever `S[mi]` equals to `e`, `lo` will increase by 1, until the `lo == hi`, that is to say `S[lo - 1]` is the element which equals to `e` and has the largest index.

Binary search is a very important and fundamental algorithm. I hope I can master it very well!

### Reference

- [Data Structure and Algorithm from Junhui Deng(Binary Search Version C)](https://dsa.cs.tsinghua.edu.cn/~deng/ds/dsacpp/index.htm/)
