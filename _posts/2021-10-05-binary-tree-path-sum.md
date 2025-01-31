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

```python
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

# @param root TreeNode类
# @param sum int整型
# @return int整型二维数组
#
class Solution:
    def pathSum(self , root , sum ):
        # write code here
        temp,res=[],[]

        def dfs(root,sum,cnt):
            if not root: return #如果节点为空结束当前递归
            temp.append(root.val) #将当前节点加入temp数组
            cnt += root.val #把当前节点加入到路径和中
            if root.left == None and root.right == None: #当递归到没有子树的时候就需要判断
                if cnt == sum:res.append(temp[:]) #如果当前节点的路径和等于sum，那么就在res中插入tmp
            else:
                dfs(root.left,sum,cnt) #递归左子树
                dfs(root.right,sum,cnt) #递归右子树

            cnt -= temp[len(temp) - 1]
            temp.pop()

        dfs(root,sum,0)
        return res
```
❗️
PS. function inside function in python, inside funtion can use the variable outside
