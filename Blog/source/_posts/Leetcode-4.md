title: Leetcode-4
author: Rabbet
tags:
  - leetcode
categories:
  - algorithm
description: Roman to Integer
date: 2020-09-28 15:10:00
---
## Question
Roman numerals are represented by seven different symbols: ```I```, ```V``` ,```X```,```L```, ```C```, ```D``` and ```M```.

|**Symbol** | **Value**|
|:--:|:--:|:--:|
|I|1|
|V|5|
|X|10|
|L|50|
|C|100|
|D|500|
|M|1000|

For example, two is written as ```II``` in Roman numeral, just two one's added together. Twelve is written as, ```XII```, which is simply ```X```+ ```II```. The number twenty seven is written as ```XXVII```, which is ```XX``` + ```V``` + ```II```.

Roman numerals are usually written largest to smallest from left to right. However, the numeral for four is not ```IIII```. Instead, the number four is written as ```IV```. Because the one is before the five we subtract it making four. The same principle applies to the number nine, which is written as ```IX```. There are six instances where subtraction is used:
  * ```I``` can be placed before ```V```(5) and ```X```(10) to make 4 and 9.
  * ```X``` can be placed before ```L```(50) and ```C```(100) to make 40 to 90.
  * ```C``` can be placed before ```D```(500) and ```M```(1000) to make 400 to 900.

Given a roman numeral, convert it to an integer. Input is guaranteed to be within the range from 1 to 3999.

**Example 1 : **
 >**Input : ** "III"
 >**Output : ** 3

**Example 2 : **
 >**Input : ** "IV"
 >**Output : ** 4

**Example 3 : ** 
 >**Input : ** "IX"
 >**Output : ** 9

**Example 4 : **
 >**Input : ** "LVIII"
 >**Output : ** 58
 >**Examplanation : ** L = 50, V = 5, III = 3

**Example 5 : **
 >**Input : ** "MCMXCIV"
 >**Output : ** 1994
 >**Examplanation : ** M = 1000, CM = 900, XC = 90, IV = 4.


## Answer

 ### 暴力破解法
 这个思路就是把每个罗马数字所对应的整数一一对应，最后再根据罗马数字的书写方式用循环套出结果。时间复杂度为O(n),空间复杂度为O(1)
```
class Solution {
public:
    int fun(char s) {
        if (s == 'I') return 1;
        if (s == 'V') return 5;
        if (s == 'X') return 10;
        if (s == 'L') return 50;
        if (s == 'C') return 100;
        if (s == 'D') return 500;
        if (s == 'M') return 1000;
        return 0;
    }
    int romanToInt(string s) {
        int res = 0;
        for (int i = 0; i < s.size();i++) {
            
            if ((i+1 < s.size()) && (fun(s[i]) < fun(s[i+1])))
                res -= fun(s[i]);
            else 
                res += fun(s[i]);
        }
        return res;
    }
};      
```
