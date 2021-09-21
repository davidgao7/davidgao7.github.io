---
title: 'count sorted vowel strings'
date: 2021-09-21
permalink: /posts/2021/09/count-vowel-strings/
tags:
  - dynamic programming
---
# 统计字典序元音字符串的数目

## 题目描述
给你一个整数`n`, 请返回长度为 `n` ，仅由元音`a`,`e`,`i`,`o`,`u` 组成且按**字典序**排列的字符串数量。

字符串 s 按 字典序排列 需要满足：对于所有有效的 i，s[i] 在字母表中的位置总是与 s[i+1] 相同或在 s[i+1] 之前。

```
输入：n = 1
输出：5
解释：仅由元音组成的 5 个字典序字符串为 ["a","e","i","o","u"]

输入：n = 2
输出：15
解释：仅由元音组成的 15 个字典序字符串为
["aa","ae","ai","ao","au","ee","ei","eo","eu","ii","io","iu","oo","ou","uu"]
注意，"ea" 不是符合题意的字符串，因为 'e' 在字母表中的位置比 'a' 靠后

输入：n = 33
输出：66045
```

## 解法一： 无脑数学
等价于把n个字母分给五种元音，且分配数目可以为零，就是求c(n+4, n) = c(n+4, 4)
```cpp
class Solution {
public:
    int countVowelStrings(int n) {
        if (n == 1) return 5;
        return (n + 4) * (n + 3) * (n + 2) * (n + 1) / 24;
    }
};
```
### 解法二： 动态规划
a可以加在（aeiou）之前，e可以加在(eiou)之前，以此类推

就是求n-1次前缀和

```cpp
class Solution {
public:
    int countVowelStrings(int n) {
        vector<int> cnt(5, 1);
        while(--n) partial_sum(begin(cnt), end(cnt), begin(cnt));
        return accumulate(begin(cnt), end(cnt), 0);
    }
};
```
