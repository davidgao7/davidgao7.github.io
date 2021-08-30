---
title: 'Max length of unique string'
date: 2021-08-20
permalink: /posts/2021/08/max-length-string/
tags:
  - python list
  - LeetCode
---
<!-- 感想 -->
> 一步一个脚印，现在就是最艰难的时刻，不要懒，不要脸往前冲就行了

## 题目描述
给定一个数组arr， 返回arr的*最长* *无重复* 子数组的长度，

---
e.g. 1

a = [1, 3, 5, 7, 9]

- [x] sublist: [1, 3]

- [x] sublist: [3, 5, 7]

- [ ] not a sublist: [1, 3, 7]

- 最长无重复子数组(maxLength)：[1, 3, 5, 7, 9]

e.g. 2

a = [2, 2, 3, 4, 3]

a_max = [2, 3, 4]

maxLength = 3

---
## 题目思路
- 一开始，我看到了`无重复`，set不会有重复，但是set不能保证你拿的是连续的，不是连续的也就不能称之为sublist
- 接着，我试了暴力解法，会超时，思路是双指针，右指针没有重复就右移， 有重复左指针向右移动一个防止漏掉前面的可能性
  - 这个解法缺点是每一次指针移动都要检查答案是否可行，每一次检查又要loop从左指针到右指针，总共需要O(mn), polynomial time.
- 首先要无重复， 那么我们一旦找到了重复的数字，由于需要return**连续**的subarray，我们就只能去掉所有在第一个重复的数的后方的所有元素

找到无重复sublist：
```Python
for i in arr:
  while i in l:
    l.pop(0)
  l.append(i)
```

之后我们在考虑怎样得到最长sublist：
- 参考dynamic programming，我们可以用max()每一次都取到最大值

```Python
res = max(res, len(l))
```
合起来：
```Python
def maxLength(self, arr):
    res = 0
    l = list()
    for i in arr:
        while i in l:  # 如果一直有，就把在重复
            print("%d in l" % i)
            l.pop(0)
            print("pop")
            print(l)
        l.append(i)  # 剔除之后再加上一个保底
        print(l)
        res = max(res, len(l))  # 一直保留最大的
```
