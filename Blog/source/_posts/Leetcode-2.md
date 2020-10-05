title: Leetcode-2
author: Rabbet
mathjax: true
tags:
 - leetcode
categories: 
 - algorithm
description: Reverse Integer
date: 2020-09-23 14:46:00
---
## Question

 Given a 32-bit signed integer, reverse digits of an integer.

 **Example 1**
 > **iput** : 123
 > **Output** : 321
 
 **Example 2**
 > **Input** : -123
 > **Output** : -321
 
 **Example 3**
 > **Input** : 120
 > **Output** : 21
 

 **Note :** 
&emsp;&emsp;Assume we are dealing with an environment which could only store integers within the 32-bit signed integer range: [$(-2)^{31}$, $2^{31}$-1]. For the purpose of this problem, assume that your function returns 0 when the reversed integer overflows.


## Answer

 ### 计算法
 这是一个比较投机的方案，因为使用了数字类型long后，就不会再有溢出的问题，最后再和INT_MAX比较一下就可以了。时间复杂度为O(nlogn)
 ```
class Solution {
public:
    int reverse(int x) {
        long res = 0;
        for (;x != 0 ; x /= 10)  res = res * 10 + x % 10;
        return (res > INT_MAX || res < INT_MIN) ? 0 : res;
    }
}
```

