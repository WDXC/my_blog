title: Leetcode-5
author: Rabbet
mathjax: true
tags:
  - leetcode
categories:
  - algorithm
description: Longest Common Prefix
date: 2020-10-03 16:23:00
---
## Question
Write a function to find the longest common prefix string amongst an array of strings.  

If there is no common prefix, return an empty string "".

 **Example 1:**
  > **Input : ** ["flower","flow","flight"]
  > **Output : ** "fl"

 **Example 2: **
  > **Input : ** ["dog","racecar","car"]
  > **Output : ** ""
  > **Explanation : ** There is no common prefix among the input strings.

  **Note : **
  All given inputs are in lowercase letters a-z.


## Answer
### 思路一
  **暴力破解法:** 首先通过循环把这个字符串中最长的一个字符设置为第一个字符串，再使用循环将这第一个字符串去和所有的字符比较，不对就输出""，对了就有ans存储并输出.时间复杂度为O($n^{2})$,空间复杂度为O(n).整体代码如下
  ```
class Solution {
public:
    string longestCommonPrefix(vector<string>& strs) {
        string ans = "";
        int n = strs.size();
        if (n == 0) return "";
        
        int l = strs[0].size();
        for (string a : strs) {
            if (l < strs.size()) {
                l = strs.size();
            }
        }
        
        int index = 0;
        
        for (char s : strs[0]) {
            for (int i = 0 ;i < n ;i++) {
                if (strs[i][index] != s || index > l)
                    return ans;
               }
            ans += s;
            index++;
        }
        return ans;
    }
};
```
### 思路二
 **排序法 : ** 首先把这个字符串用sort函数从小到达排序一遍，然后选择第一个和最后一个,比较他们是否存在公共字符就可以了(选择第一个和最后一个，是因为他们的区别是最大的，可以更加快速的得到结果),最后我们只需要比较有多少公共字符就行了. 时间复杂度为O(n)，空间复杂度为O(n).具体代码如下:
 ```
class Solution {
public:
    string longestCommonPrefix(vector<string>& strs) {
        string ans = "";
        int n = strs.size();
        if (n == 0) return ans;
        
        sort(strs.begin(),strs.end());
        string a = strs[0];
        string b = strs[n-1];
        
        for (int i = 0 ; i < a.size() ; i++) {
            if (a[i] == b[i]) {
                ans += a[i];
            }
            else
                break;
        }
        return ans;
    }
};
```
