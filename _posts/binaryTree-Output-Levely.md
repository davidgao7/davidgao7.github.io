---
title: 'Blog Post number 2'
date: 2021-08-16
permalink: /posts/2021/08/binaryTree-levely-output/
tags:
  - Binary tree
  - Inorder traversal
  - LeetCode
---
今天得按要求完成两道medium/一道hard，目前搞透了一道medium， 先把这道题知识沉淀一下。晚上再打卡总结一下今天的收获（估计就偷个懒Crtl C + Crtl V）。

## 题目描述
给你一个二叉树，要求一层一层get这个二叉树的层序遍历的结果

e.g. Given binary tree: {3,9,20,#,#,15,7}， 在code里是OOP的Tree来写的

```python
T = TreeNode(3)
T.left = TreeNode(9)
T.right = TreeNode(20)
T.right.left = TreeNode(15)
T.right.right = TreeNode(7)
```
Tree图

![binary tree example](/images/levely_binary_tree.png)

in order traversal result:

```
[
  [3],
  [9, 20],
  [15, 7]
]
```
需要注意TreeNode的定义，没有child的情况child为`None`.

## 题目思路
- 无论何时都得照顾好base case
  * 如果给的tree结构里一个node也没有，我们不用担心什么，直接return 空[]
  ```python
  class Solution:
      def levelOrder(self, root):
        if not root:
          return []
  ```
- 之后， 我们用python list.pop(index=)来拿到我们想要的current node。 注意一下 **pop()** 和 **pop(0)** 的区别
  * **pop()** 是取list中最后一个元素
  * **pop(0)** 是取list中1st元素
  ```
  >>> a = [1,2,3]
  >>> print(a.pop())
  3
  >>> print(a.pop(0))
  1
  >>>
  ```
<font color=green>Note: </font>
平时用不太熟悉的语言时遇到不确定的语法可以到terminal上玩一下当作测试，也节省了上网查找浪费的时间


- 注意append node的顺序，我们首先append left child 然后 right child， 因为我们是被要求一层一层从左到右存放的
```python
if curnode.left: queue.append(curnode.left)
if curnode.right: queue.append(curnode.right)
```
这个过程是在遍历时先去左边的树再去右边的。按照题目规定**每层**print时要从左往右储存。

问：怎样解决每层打印/储存的？<br/>
答：while loop的发动条件是quene里还有东西(听起来像打开反击陷阱...)，如果有，就遍历quene长度的次数<br/>
quene就pop第0个， 把这个node的值保存。 <br/>

在这一block我们专注解决一层, 连起来看看我们在干嘛
```python
length = len(quene)
in_list = []

for _ in range(length):
  curnode = quene.pop(0) # 移除第一个，因为是从上往下遍历
  in_list.append(curnode.val) # 拿值

  if curnode.left: quene.append(curnode.left) # store left
  if curnode.right: quene.append(curnode.right) # store right

outlist.append(in_list)
```
首先看 `for`
```python
for _ in range(length):
  curnode = quene.pop(0) # 移除第一个，因为是从上往下遍历
  in_list.append(curnode.val) # 拿值

  if curnode.left: quene.append(curnode.left) # store left
  if curnode.right: quene.append(curnode.right) # store right
```
我们在干嘛？

首先loop每一层node的个数的次数（假设次数为N，方便引用），然后pop掉**第一个**quene里的node。还记得我们第一次第一个存的什么吗？是root，所以我们第一次就顺利把第一个正确拿下来了。
接着我们往quene里存放他的left child 和 right child。

```python
if curnode.left: quene.append(curnode.left) # store left
if curnode.right: quene.append(curnode.right) # store right
```
这里我们先存left再存right， 因为我们pop的时候先pop第0个(left)，这样确保了我们永远都从左到右拿value

最后，我们把这一层放到总list里

```python
out_list.append(in_list)
```
组合起来：
```python
length = len(quene)
in_list = []
for _ in range(length):
    curnode = quene.pop(0)  # （默认移除列表最后一个元素）这里需要移除队列最头上的那个
    in_list.append(curnode.val) # 1st get left val, then got right val: [level0:l, level1:l,r, level2:l,r...]
    if curnode.left: quene.append(curnode.left) # first store left then right, same with in order
    if curnode.right: quene.append(curnode.right)
out_list.append(in_list)
```
层序遍历逻辑结束了，那么如何确定程序结束条件呢？</br>
答： 在python里，当[]是空的可以直接退出loop（真方便。。）

接着就得到遍历结果了
## 类似题目
- [102] 二叉树的层序遍历
- [107] 二叉树的层次遍历II
- [199] 二叉树的右视图
- [637] 二叉树的层平均值
- [429] N叉树的前序遍历
- [515] 在每个树行中找最大值
- [116] 填充每个节点的下一个右侧节点指针
- [117] 填充每个节点的下一个右侧节点指针II
- [104] 二叉树的最大深度
- [111] 二叉树的最小深度

<font color=red>按类分题，一次打通！</font>
