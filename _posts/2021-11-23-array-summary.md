# 数组

> 数组是存放在连续内存空间上的相同类型数据的组合


- 数组内存空间的地址是连续的

<img src='https://code-thinking.cdn.bcebos.com/pics/%E7%AE%97%E6%B3%95%E9%80%9A%E5%85%B3%E6%95%B0%E7%BB%84.png' width=600> </img></div>

- 正是因为**数组的在内存空间的地址是连续的， 所以我们在删除或者增添元素的时候， 难免要移动其他元素的地址**

<img src='https://code-thinking.cdn.bcebos.com/pics/%E7%AE%97%E6%B3%95%E9%80%9A%E5%85%B3%E6%95%B0%E7%BB%841.png' width=600> </img></div>

- 二维数组

<img src='https://code-thinking.cdn.bcebos.com/pics/%E7%AE%97%E6%B3%95%E9%80%9A%E5%85%B3%E6%95%B0%E7%BB%842.png' width=600> </img></div>

**二维数据在内存中不是 `3*4` 的连续地址空间，而是四条连续的地址空间组成！**

## 经典例题
- [704] [二分查找](https://leetcode-cn.com/problems/binary-search/)
- [27] [移除元素](https://leetcode-cn.com/problems/remove-element/) (双指针)
- [209] [长度最小的子数组](https://leetcode-cn.com/problems/minimum-size-subarray-sum/) (滑动窗口)

- [数组：这个循环可以转懵很多人！](https://programmercarl.com/0059.螺旋矩阵II.html)
>模拟类的题目在数组中很常见，不涉及到什么算法，就是单纯的模拟，十分考察大家对代码的掌控能力。
在这道题目中，我们再一次介绍到了**循环不变量原则**，其实这也是写程序中的重要原则。
相信大家又遇到过这种情况： 感觉题目的边界调节超多，一波接着一波的判断，找边界，踩了东墙补西墙，好不容易运行通过了，代码写的十分冗余，毫无章法，其实**真正解决题目的代码都是简洁的，或者有原则性的**，大家可以在这道题目中体会到这一点。


#### source
代码随想录螺旋矩阵，这题蛮绕的，多看看
