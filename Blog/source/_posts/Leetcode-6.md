title: Leetcode-6
author: Rabbet
mathjax: true
tags:
  - leetcode
categories:
  - algorithm
description:  Valid Parentheses
date: 2020-10-04 07:53:00
---
## Question
Given a string s containing just the characters ```'('```,``` ')'```,``` '{'```,``` '}'```,``` '['``` and``` ']'```, determine if the input string is valid.
An input string is valid if:
  1. Open brackets must be closed by the same type of brackets.
  2. Open brackets must be closed in the correct order.

**Example 1: ** 
   > **Input: ** s = "()"
   > **Output: ** true


**Example 2: **
  > **Input: ** s = "()[]{}"
  > **Output: ** true


**Example 3: **
  > **Input: ** s = "(]"
  > **Output: ** false


**Example 4: **
  > **Input: ** s = "([)]"
  > **Output: ** false


**Example 5: **
  > **Input: ** s = "{[]}"
  > **Output: ** true


**Constraints:**
  * 1 <= s.length() <= $10^{4}$
  * s consists of parentheses only ```'()[]{}'```


## Answer
### 思路一
  **堆栈法 : ** 首先把有效括号的左半边先入栈，再来看右半边括号，首先需要判断我们堆栈是否为空，或者是否是匹配的括号。如果是，那就直接输出false。如果不是就出栈，在最后判断一下这个数组是否为空，因为如果全部出栈那么这个stack就是空的。如果不是，那么就不是空，就要输出false。时间复杂度为O(n),具体代码如下：
  ```
class Solution {
public:
    bool Pair(char begin,char end) {
        if (begin == '(' && end == ')')
            return true;
        if (begin == '[' && end == ']') 
            return true;
        if (begin == '{' && end == '}') 
            return true;
        
        return false;
    }
    bool isValid(string s) {
        stack<char> res;
        for (int i = 0 ; i < s.size() ; i++) {
            if (s[i] == '(' || s[i] == '[' || s[i] == '{')
                res.push(s[i]);
            if (s[i] == ')' || s[i] == ']' || s[i] == '}') {
                if (res.empty() || !Pair(res.top(),s[i]))
                    return false;
                else 
                    res.pop();
            }
        }
        return res.empty();
    }
};
```
  **简化版堆栈法 : ** 不需要用函数来判断括号是否匹配，直接在switch语句中判断好，时间复杂度为O(n),不过switch相对于if-else所需的空间更多，具体代码如下：
  ```
  class Solution {
public:
    bool isValid(string s) {
       stack<char> res;
        for (char& c : s) {
            switch (c) {
                case '(': 
                case '[': 
                case '{': res.push(c);break;
                case ')': if (res.empty() || res.top() != '(') return false; else res.pop();break;
                case ']': if (res.empty() || res.top() != '[') return false; else res.pop();break;
                case '}': if (res.empty() || res.top() != '{') return false; else res.pop();break;
                default: ;
            }
        }
        return res.empty();
    }
};
```
### 思路二
  **AscII值相减 : ** 时间复杂度为O(n),空间复杂度为O(1),具体代码如下:
  ```
class Solution {
public:
    bool isValid(string s) {
        int n= 0;
        for (char a : s) {
             if (n && ((a - s[n-1]+1)/2 == 1))
                n--;
            else 
                s[n++] = a;
        }
        return !n;
    }
};
```
