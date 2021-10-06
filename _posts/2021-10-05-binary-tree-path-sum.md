---
title: 'Binary Tree Path Sum'
date: 2021-09-24
permalink: /posts/2021/09/path-sum/
tags:
  - binary tree
  - depth first search
  - breath first search
---
## 题目描述
给定一个节点数为 n 的二叉树和一个值 sum ，请找出所有的根节点到叶子节点的节点值之和等于的路径，如果没有则返回空。

例如：
给出如下的二叉树，sum = 22 ，

given:
![binary tree](/images/pathSumEg.png)

return
```
[
  [5,4,11,2],
  [5,8,9]
]
```
*Space complexity: O(n)*

*Time complexity: O(n)*

## 解题思路
题目是想让你一条一条路径找到和为sum的路径们，那我们学过的bfs(breath first search) 和 dfs(depth first search) 趁现在来复习一下

Here's the definition of BFS (ch 22.2 Introduction to Algorithms):
> Given a graph G = (V,E) and a distinguished **source** vertex s, breadth-first search systematically explores the edges of G to 'discover' every vertex that is **reachable** from s.

“找到能通向罗马的所有路”

<font color=red>BFS作用：</font> For any vertex v reachable from s, the simple path in the breadth-first tree from s to v corresponds to a **shortest path** from s to v in G.

Here is how bfs process

![bfs mov](/images/BFS-Process.png)

BFS逻辑思路：

given: G = (V,E) with adjacency lists of weights
![bfs alg](/images/BFSAlg.png)

```
scanning adjacency lists: O(E)
queue operation: O(V)
BFS: O(V+E)
```

---
DFS逻辑思路：
*To search "deeper" in the graph whenever possible*.

> DFS 找到最近经历的 vertex v， 找到与 v 连接的所有 edges。一直找直到我们找到了所有能从原点出发 reach 到的 vertices。

> 如果有一些没有找到的vertices， dfs 继续选择另一个vertex当作source， 继续重复dfs

> DFS 一直重复到它发现了所有的 vertex

<font color=red>DFS作用：</font>

Here is how dfs process

![dfs mov](/images/DFS-Process.png)

DFS逻辑：

![dfs alg](/images/DFSAlg.png)

```
Enqueuing / Dequeuing : O(1)
Queue operation : O(V)
Scanning adjacency lists: O(E)
DFS: O(V+E)
```
