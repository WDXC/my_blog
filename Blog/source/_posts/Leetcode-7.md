title: Leetcode-7
author: Rabbet
mathjax: true
tags:
  - leetcode
categories:
  - algorithm
description: Merge Two Sorted Lists
date: 2020-10-04 10:08:00
---
## Question
Merge two sorted linked lists and return it as a new sorted list. The new list should be made by splicing together the nodes of the first two lists.

**Example 1 : **
  ![avatar](https://assets.leetcode.com/uploads/2020/10/03/merge_ex1.jpg)
  > **Input : ** l1 = [1,2,4],l2 = [1,3,4]
  > **Output : ** [1,1,2,3,4,4]


**Example 2 : **
  > **Input : ** l1 = [], l2 = []
  > **Output : ** []


**Example 3 : ** 
  > **Input : ** l1 = [], l2 = [0]
  > **Output : ** [0]


**Constraints : **
  * The number of nodes in both lists is in the range ```[0, 50]```.
  * ```-100 <= Node.val <= 100```
  * Both ```l1``` and ```l2``` are sorted in **non-decreasing** order.


## Answer

### 思路一
  **递归法 : ** 首先判断两个链表中的一个是否为空，如果有一个为空，那么就以这个链表为输出结果。为了保存其他两个链表，我就需要新建一个链表。因为要顺序保存，所有通过值大小的比较存入t，作t的头节点。之后t->next用递归的方式依次存入。时间复杂度为O(n),具体代码如下:
  ```
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        if (!l1) return l2;
        if (!l2) return l1;
        
        ListNode* t;
        if (l1->val < l2->val) {
            t = l1;
            l1 = l1->next;
        }
        
        else {
            t = l2;
            l2 = l2->next;
        }
        
        t->next = mergeTwoLists(l1,l2);
        return t;
    }
};
```
