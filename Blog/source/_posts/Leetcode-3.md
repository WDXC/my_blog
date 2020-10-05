title: Leetcode-3
author: Rabbet
tags:
  - leetcode
categories:
  - algorithm
description: Palidrome Number
date: 2020-09-25 13:31:00
---
## Question
 Determine whether an integer is a palindrome. An integer is a palindrome when it reads the same backward as forward. 

 **Example 1** 
 > **Input : ** 121
 > **Output : ** true
 

 **Example 2**
 > **Input : ** -121
 > **Output : ** false
 > **Explanation : ** From left to right, it reads -121. From right to left, it becomes 121-. Therefore it is not a palindrome.  

 
 **Example 3**
 > **Input : ** 10
 > **Output : ** false
 > **Explanation : ** Reads 01 from right to left. Therefore it is not a palindrome.


## Answer

### 思路一
  简单的把数字进行一个逆转，最后判断反转后的数字和原来的数字是否一样。时间复杂度O(n)
  ```
class Solution {
public:
    bool isPalindrome(int x) {
        if (x < 0) return false;
        long res = 0;
        long s = x;
        for (;s != 0 ; s /=10)  res = res * 10 + s %10;
        return (res == x) ? true : false;
    }
};
```

### 思路二
我们可以不需要等数字全逆转结束，只需要逆转一半看是否符合条件就可以了
  * 如何一半停止
    * 如果 x<=r 时就可以停止了
    * 如果是偶数长度，并且是回文，那么 x == r
    * 如果是奇数长度，并且是回文，那么 x < r，这时候r比x多一位数

  * 停止后判断是否是回文
    * 如果偶数长度，判断 r == x;
    * 如果奇数长度，判断 r/10 == x;
  
  时间复杂度为O(n)
  ```
class Solution {
public:
    bool isPalindrome(int x) {
        if (x < 0 || (x != 0 && x %10 == 0)) return false;
        int res = 0;
        while (x > res) {
            res = res * 10 + x % 10;
            x /= 10;
        }
        return (res == x) || (res/10 == x);
    }
};
```
