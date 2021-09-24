---
title: 'Find Kth Largest'
date: 2021-09-24
permalink: /posts/2021/09/find-kth-largest/
tags:
  - arrays
  - divide and conquer
  - quick select
  - sorting
  - heap (priority heap)
---
## 题目描述
- 经典题目

给定整数数组 nums 和整数 k，请返回数组中第 k 个最大的元素。

请注意，你需要找的是数组排序后的第 k 个最大的元素，而不是第 k 个不同的元素。

```
示例 1:


输入: [3,2,1,5,6,4] 和 k = 2
输出: 5


示例 2:


输入: [3,2,3,1,2,4,5,5,6] 和 k = 4
输出: 4



提示：


1 <= k <= nums.length <= 10⁴
-10⁴ <= nums[i] <= 10⁴
```

```python
class Solution:
    def findKthLargest(self, nums: List[int], k: int) -> int:
        # write code here
        # quick select

        # choosinig pivoit
        n = len(nums)
        pivoit = n - 1

        # divide
        left = [x for x in nums if x > nums[pivoit]]  # remember to use a[pivoit] instead of pivoit which is a index not actual number!
        mid = [x for x in nums if x == nums[pivoit]]
        right = [x for x in nums if x < nums[pivoit]]  # find the largest first 从大到小

        l, m, r = len(left), len(mid), len(right)
        # if k in the left arr
        if k <= l:
            return self.findKthLargest(left, k)
        # if k on the right side
        elif k > l + m:
            return self.findKthLargest(right, k - (l + m))
        # otherwise it means the mid # is the kth largest
        else:
            return mid[0]
```
