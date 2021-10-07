---
title: 'Copy Random List'
date: 2021-10-07
permalink: /posts/2021/10/copy-random-list/
tags:
  - hash table
  - linked list
---
## 题目描述
请实现 `copyRandomList` 函数，复制一个复杂链表。在复杂链表中，每个节点除了有一个 next 指针指向下一个节点，还有一个 `random` 指针指向链表中的任意节点或者 `null`。

## 解题思路
乍得一看很迷惑的题, 我们直接return head行不行？ 不行。这样address和原linkedlist都是一样的，题目就会知道你在搞事情。

那么我们现在就明确了目标：deep copy一个list， 根据题目定义，这个list的structure为

```cpp
class Node{
public:
    int val;
    Node* next;
    Node* random;

    Node(int _val){
      val = _val;
      next = NULL;
      random = NULL;
    }
}
```
**PS.** 在 C++11里，没有`NULL`，我们统一用`nullptr`。

```cpp
class Node{
public:
    int val;
    Node* next;
    Node* random;

    Node(int _val){
      val = _val;
      next = nullptr;
      random = nullptr;
    }
}
```

来看看我们怎么copy这个list的：这个list向linkedlist，我们做的时候还是不要忘记之前对linkedlist的操作

```c++
Node* copyRandomList(Node* head){
  // 带 * 就是货真价实的object
  // & address of *

  // 1.经典开局：如果你不给，我就不要
  if (head == nullptr) return nullptr

  // 2. setup：找到能储存原本list顺序关系的 data structure
  std::unordered_map<Node *, Node *> map;
  // large table-> std::unordered_map, small table(under 100 elements)->std::map because it reads in O(log n)
  // if going to change table a lot -> std::map

  //3. 把原先的list里的node关系转移到map里
  cur = head;
  while (cur != nullptr) {
    map[cur] = new Node(cur->val); // broke the node connection, store into map
    cur = cur->next;
  }
    cur = head;
}

  // return head
  return map[head];
```
