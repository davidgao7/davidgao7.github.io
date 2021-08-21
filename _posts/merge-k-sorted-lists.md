---
title: 'Merge k sorted Linked lists'
date: 2021-08-20
permalink: /posts/2021/08/merge-k-sorted-lists/
tags:
  - Linked List
  - Priority Queue
  - LeetCode
---
<!-- 感想 -->
就这一道题揪出了我的短板，虽然一直被强调什么语言都无所谓，能用就行，但是没有pointer我就不知道怎么更新了，这回有ptr的语言和没有的我都写，都好好理解一下，看看到底有什么“难处”！

*这鬼题花了我两天时间！不好好整理一下（语言和思路）都对不起这时间！*

为了补偿自己花费的更多时间，今天写两种方法
<!-- 感想 -->
## 题目描述
Given k sorted linked lists, combine them into a single linked list.

Here's an example:
```
Given
l1: 1 -> 2 -> 5
l2: 8 -> 0 -> 3
l3: 3 -> 4

return
l: 0 -> 1 -> 2 -> 3 -> 3 -> 4 -> 5 -> 8
```
## 题目思路
Different from regular sorting problem, we are having linked lists, which are user
defined structure, we can't have as much freedom as we did when we have the regular
data structure like arrays or lists.
We can expected that we will spend some time on thinking how we update element.

由于linked list是 user defined，限制增多，广义上我们可以摒弃定义用现成的list使之更灵活，也可以运用某些语言中的pointer特性方便的更新linked list

解决完这个后，我们来复习一下pointer

我一开始学的java， pointer不熟，趁现在恶补一下

- & stands for address referencing
- for *single value*
```cpp
int n;
int* p = &n;     // pointer to n
int& r = *p;     // reference is bound to the lvalue expression that identifies n
r = 7;           // stores the int 7 in n
prinf("%d", *p); // lvalue-to-rvalue implicit conversion reads the value from n
```
returns
```
7
```
- for *array*
```cpp
int a[2];
int* p1 = a; // pointer to the first element a[0] (an int) of the array a
int b[6][3][8];
int (*p2)[3][8] = b; // pointer to the first element b[0] of the array b,
                     // which is an array of 3 arrays of 8 ints
```
- for *object*
  * Because of the [derived-to-base](en.cppreference.com/w/cpp/language/implicit_cast.html) implicit conversion for pointers, pointer to a base class can be initialized with the address of a derived class

  ```cpp
  struct Base {};
  struct Derived : Base {};
  Derived d;
  Base* p = &d;
  ```

*PS. 入门应该学C的，即使预计会到明年毕业。。*

### 方法一： Language with pointer
- cpp: Merge sort like,

### 方法二： Language without pointer
- python:

## 类似题目
- [归并排序](https://www.nowcoder.com/practice/23ed40416d9c4c72816edb12daa3bdff?sourceQid=724&sourceTpId=196)
- [链表合并](https://www.nowcoder.com/practice/27c833289e5f4f5e9ba3718ce9136759?sourceQid=724&sourceTpId=196)
- [最小区间](https://www.nowcoder.com/practice/65cfde9e5b9b4cf2b6bafa5f3ef33fa6?tpId=196&&tqId=37081&rp=1&ru=/activity/oj&qru=/ta/job-code-total/question-ranking)
- [查找第k大的元素](https://www.nowcoder.com/practice/673454422d1b4a168aed31e449d87c00?sourceQid=724&sourceTpId=196)
- [找出单向链表中的一个节点，该节点到尾指针的距离为k](https://www.nowcoder.com/practice/65cfde9e5b9b4cf2b6bafa5f3ef33fa6?tpId=196&&tqId=37081&rp=1&ru=/activity/oj&qru=/ta/job-code-total/question-ranking)
- [非递归实现binary search](https://www.nowcoder.com/practice/c953813dd1aa4eacbc3d403dff60a23a?sourceQid=724&sourceTpId=196)

 ```
 ps. 偶然在GitHub上看到的，喜欢自己造轮子什么时候成了缺点了？
 合着我机器学习白上了？就非得套Tensorflow，pytorch，sklearn？
 没加法哪来的乘法？
 就是要自己先造轮子才能造出更好的轮子！
 ```
