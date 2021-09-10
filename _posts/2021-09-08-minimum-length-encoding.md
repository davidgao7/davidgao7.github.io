---
title: '单词的压缩编码'
date: 2021-09-08
permalink: /posts/2021/09/minimum-length-encoding/
tags:
  - dictionary
  - array
  - hash
  - string
---
## 题目描述
Array `words` 的**有效编码**由任意 string 和下标数组`indices`组成，
满足：
  - `words.length == indices.length`
  - 助级 string `s` 以 `'#'` 结尾
  - 对于每个下标 `indices[i]`, `s`的一个从`indices[i]` 开始，到下一个`'#'` 字符结束（但不包括 `'#'`）的 **子字符串** 恰好与 `words[i]` 相等

给你一个单词数组 `words`, 返回成功对 `words` 进行编码的**最小** 助记字符串 `s` 的长度。

Example 1
```
Input: words = ["time", "me", "bell"]
Output: 10

解释：
有效编码为 “time#bell#” , indices = [0, 2, 5]

words[0] = "time", indices = 0，substring 从 index 0 开始
words[1] = "me", the substring of s starting from indices[1] = 2
to the next '#' is in "ti[me]#bell#"
words[2] = "bell", start from indices[2] = 5 to the next '#' is in "time#[bell]#"
```
Example 2
```
words = ["t"]
Output: 2
s = "t#" indices = [0]
```

## 思路
```java
class Solution{
  public int minimumLengthEncoding(String[] words){
    // 1. sort the string arr based on length of String
    // longer string are more likely be in the encoding since
    // shorter string will be more likely included in longer string
    Arrays.sort(words, (a,b) -> b.length()-a.length());

    // 2. create a string of valid encoding
    StringBuilder encoding = new StringBuilder();

    for(String s: words){
      if(encoding.indexOf(s + "#") == -1){ // check string + # appears in the encoding or not(-1)
        encoding.append(s+"#"); // if not , add
      }
    }
    return encoding.length();
  }
}
```
