---
title: 'Blog Post number 3'
date: 2021-08-25
permalink: /posts/2021/08/bst-vs-heap/
tags:
  - Binary search tree
  - Heap
---
# Binary Search Tree vs. Heap
Can't remember what's the difference between heap & BST all the sudden...

## What we should know
- Definition
- Big-O complexity

## Definition
> <font color=red>Binary Search Tree</font> is a data structure that allows for fast **insertion**, **removal**, and **lookup** of items while offering an *efficient* way to iterate them in *sorted* order

> <font color=red>Heap</font> is a **complete** binary tree

What is a `complete binary tree`?
> A <font color=red>complete</font> binary tree is a **balanced** binary tree

What is a `balanced binary tree`?
> A <font color=red>balanced</font> [binary tree has its left and right subtrees of every node differ in height by no more than 1](https://leetcode.com/problems/balanced-binary-tree)

What is tree's `height` / `depth`?
> The **depth** of a node is the number of edges from the node to tree's root node

- The <font color=blue>root</font> node will have a depth of <font color=red>0</font>

> The **height** of a node is the number of edges on hte *longest* path from the <font color=red>node</font> to <font color=red>a leaf</font>
- A <font color=blue>leaf</font> node will have a height of <font color=red>0</font>

## Complexity
### binary search tree
- `Lookup`, `insertion`, `removal` : <font color=red>O(logn)</font> since we can discard half of the tree at each step, according to the input value being greater or less than the one in the current node
  - Lookup
  ![BST-Lookup](/images/BST-Lookup.png)
  - Insertion
  ![BST-Insertion](/images/BST-Insertion.png)
  - Traversal

    <font color=red>O(n)</font> --> n nodes in the tree, each one of them only visited once

### Heap
- A *Node* is at level *k* if distance between this node and the root node is *k*
- **Maximum** possible number fo nodes at level k is 2^k
- Usually, the heap is filled from **top to bottom**, at each layer, it is filled from **left to right**.
- As we can see that heap is *not sorted*, we can make it sorted by removing root node from the tree n times:
  - This is also called **heap sort**
  - Time Complexity: O(nlogn)


### 一图展示
![heap_bst_time_compare](/images/heap-bst-time.png)
---
![BST](/images/BST.jpg)
Binary Search Tree

---
![Heap](/images/Heaps.jpg)
Heap

Left: Min-Heap (Smallest on the top)  
Right: Max-Heap (Largest on the top)

> 主要 difference： BST 不允许 duplicates; heap 不是 sorted

## Reference<img src="/images/link.jpeg" width="20" height="25">
- https://www.baeldung.com/cs/heap-vs-binary-search-tree
- https://www.baeldung.com/cs/binary-search-trees
- https://stackoverflow.com/questions/6147242/heap-vs-binary-search-tree-bst
