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
l2: 0 -> 8 -> 3
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
- \* stands for a pointer declaration
---
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

*PS. 入门应该学 C的，即使预计会到明年毕业。。*

### 中心思想： Pointer(or pointer like)
- 换汤不换药，终究是个排序题
- 那说到排序题，什么space/time complexity，是不是又要整一堆？
- 为什么面试会问你mergesort？

我现在的sorting都是基于二分法：即把原先的container(array, list, vector...) 拆开分成几部然后单个排序，接着合成最终答案。如果你记不住，两句话就是‘解决不了大困难，我还解决不了小困难吗?’，‘解决了真么多小困难，那还有大困难吗?’。

### 定义
我们首先来看题目是怎么定义一个node的

Python:
```python
class ListNode
  def __init__(self, val=0, next=None):
    self.val = val
    self.next = next
```

C++:
```cpp
struct ListNode{
  int val;
  ListNode* next;
}// Node structure
```

我刚开始没感觉有什么不同，然后在遍历linked list时意识到python没有pointer，都是object。那咋整？不急，python比cpp“聪明”，他会自己判断是不是pointer

其实定义的时候，就只有一行不同：

```cpp
ListNode result(0); //.......(1a)
ListNode *ptr = &result;//...(2b)
```

```python
dummy = ListNode(-1) #.......(1a)
x = dummy            #.......(2b)
```

主要来看每个block的（2b）行，在cpp中我们用了一个pointer指向result node的address。

在ptr变化的同时，result也会同时变化。

### 题解
在理解了怎样manipulate linked list之后，我们来想想解法。

我们有
```
l1: 1 -> 2 -> 5
l2: 0 -> 8 -> 3
l3: 3 -> 4
```
每一个sublist都是有序的，我们需要合成一个大list，似曾相识？对，mergesort！

1. 首先确定框架
  - 把一整个list换成merge n 个小lists
  - 我们可以不用真的把 list 拆成小 list ，可以用 left , right 做为 index 指向我们想要的首尾

C++:
```cpp
ListNode *merge(std::vector<ListNode*> &lists, int left, int right){
  // ***base case***

  // 如果你想合并的左手边的list变到了右手边，说明没有list让你继续玩了
  if (left > right) return nullptr;

  // 如果你想合并的两个list重叠了，选一个list return就行
  if (left == right) return lists[left];

  // 如果你左边踏一步就到了右边，说明只剩两个lists了，直接合并
  if (left + 1 == right) return mergeTwoLists(lists[left], lists[right]);

  // divide & conquer
  // merge 的基本概念（在mergesort文章里有详细讲）
  int mid = int(left + (right - left)/2);
  ListNode *r1 = merge(lists, left, mid);
  ListNode *r2 = merge(lists, mid+1, right);

  // merge the result sublist
  ListNode *result = mergeTwoLists(r1, r2);
  return result;
}
```
同样的，我们看看python：我使用了暴力求解，直接一个一个连接, 与mergesort区分

```python
def mergeKLists(self, lists: List[ListNode]) -> ListNode:
    x = None  # 相当于nullptr, 从什么都没有开始合并
    for y in lists:
        x = self.merge(x, y)  # [ListNode1, ListNode2...], 从左到右两个两个合并
    return x  # 每次合并用mergesort
```

接着我们来看基本的两个linkedlist合并：

C++
```cpp
ListNode *mergeTwoLists(ListNode *l1, ListNode *l2) {

    // 首先创建一个‘傀儡’同步更新result
    ListNode result(0); // new object in memory
    ListNode *ptr = &result; // ptr to result memory location

    // 接着合并两个list，结果更新到result里
    // 这个时候我们的傀儡起作用了，像我们上文说的一样，pointer是指向一个memeory
    // address的，如果在这个地方住的东西变化，那么我们的indicator（ptr）指向的值
    // 也会同步变化

    // 还有一个关键的点是如果我不断更新ptr指向的Node，如果我有另一个object一直代表
    // 起点的头的话，那么这个头之后的linked list就会是一个更新后的linked list

    while (l1 && l2){ // 确保还有值能比较
      if (l1->val < l2->val){ // -> ptr 里的 attribute， . object 里的 attribute

        ptr->next = l1; // 从小到大，先拿小的
        l1 = l1->next; // 被拿的继续看下一个
      }
      else
      {
        ptr->next = l2;
        l2 = l2->next;
      }
    }
    // 注意，因为while的停止条件是：当有一个list没东西了
    // 所以我们还要处理剩下的 values

    // 剩下的 values肯定比我们已经合并的list的每一个要大（或者至少等于）
    // 所以我们直接把它接到我们更新的result的末尾
    // 这里的result是ptr，因为我们用它来update result
    if(l1) ptr->next = l1;
    if(l2) ptr->next = l2;

    // 我们result是以 0 开头定义的，只是为了建造object，与更新的linked list没有关系
    // 所以在给结果的时候把第一个node拿掉
    return result.next

    // for checking
    //printf("\nmergeTwoLists\n");
    //printNodeval(result.next);
}
```
同样的，我们来看看python
```python
def merge(self, a: ListNode, b: ListNode) -> ListNode:
  dummy = ListNode(-1)
        x = dummy  # x 是 dummy 的 ptr， 更新它会使得dummy一块更新，但是dummy一直指向第一个元素所以不会最后return空元素list！！
        while a and b:  # 每次比较都把小的放进去
            ############################################## determine next val in result,
            if a.val < b.val:                           ## continuing update ptr x to
                x.next = a                              ## append next node in
                a = a.next                              ##
            else:                                       ##
                x.next = b  # x 是dummy的ptr             ##
                b = b.next                              ##
            x = x.next                                  ## 把dummy开头的 -1 拿掉了，并且更新dummy，把之前的都去掉只给dummy要的
            ##############################################
        if a: ############################################ 处理｜a-b｜多的
            x.next = a                                   #
        if b:                                            #
            x.next = b                                   #
            ##############################################
        return dummy.next
```

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
