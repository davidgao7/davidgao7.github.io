---
title: '在二叉树中找到两个节点的最近公共祖先'
date: 2021-08-31
permalink: /posts/2021/08/lowest-common-ancestor/
tags:
  - Binary Tree
  - LeetCode
---
<!-- 感想 -->
## 题目描述
给定一棵二叉树(保证非空)以及这棵树上的两个节点对应的val值 o1 和 o2，请找到 o1 和 o2 的最近公共祖先节点。
注：本题保证二叉树中每个节点的val值均不相同。
```
e.g.
输入：[3,5,1,6,2,0,8,#,#,7,4],5,1
输出：3
```
图例：
![bst](/images/common-ancestors.png)



## 题目思路
做这道题首先得理解潜在意思：两个节点的最近公共祖先

题目要求查找的两个节点为
- 5
- 1

从图上我们可以知道距离5，1上方最近的是3，也就是说Node 5 与 Node 3 的common ancestor是3

```python
    # bottom up lookup
    # post order : L R N
    # common ancestor: node.left=o1 and node.right=o2 or inverse
    # we can check L=o1,R=o2, then take the Node N using post order traversal

    # base case
    # 如果在root找到o1 or o2 or null, 说明此时root为祖先
    if root == None or root.val == o1 or root.val == o2:
        return root

    # 左右subtree两个方向一起找,看看在左subtree还是右subtree
    left = self.helper(root.left, o1, o2)  # L
    right = self.helper(root.right, o1, o2)  # R

    # 如果其中一边有，recursive的值要通过非Null的来返回，所以return非Null值
    # NOTE：not left <===> left == None
    if not left: return right
    if not right: return left

    #         if left == None: return right
    #         if right == None: return left

    # 如果都没有，就返回啥都没有
    # elif not left and not right: 这代表两个都是空，说明没做到，本身就是空的，return就行
    return root
```
