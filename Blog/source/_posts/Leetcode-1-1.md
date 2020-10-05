title: Leetcode-1
author: Rabbet
mathjax: true
tags:
  - leetcode
categories:
  - algorithm
description: Two Sums
date: 2020-01-12 16:46:00
---
## Qestion

Give an array of intergets ```nums``` and an integer ```target```,return indices of the two numbers such that they add up to ```target```.  
You may assume that each input would have exctly one solution,and you may use the same element twice.  
You can return the answer in any order.  

 **Example 1**

 > **Input** : nums [2,7,11,15] , target = 9
 > **Output** : [0,1]
 > **Output** :Because nums[0] + nums[1] == 9, we return [0,1].

 **Examp 2**

  > **Input** : nums[3,2,4],target = 6
  > **Output** : [1,2]

 **Example 3**

  > **Input** : nums = [3,3],target = 6
  > **Output** : [0,1]

 **ConStraints**
  > * 2 <= nums.length <= $ 2^{10} $
  > * $-10^{9}$<= nums[i] <= $ 10^{9} $
  > * $-10^{9}$ <= target <= $ 10^{9} $
  > * **Only one valid anser exits.**

## Answer
 ###  hash法
  利用unordered_map数组构造映射,遍历nums[i]时，看target-nums[i]是否存在于hash表中
  时间复杂度 O(n),空间复杂度O(n)
```
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int, int> indices;
        for (int i = 0; i < nums.size(); i++) {
            if (indices.find(target - nums[i]) != indices.end()) {
                return {indices[target - nums[i]], i};
            }
            indices[nums[i]] = i;
        }
        return {};
    }
};
```

 ### 暴力破解法
  暴力破解时间复杂度O($n^{2}$),空间复杂度O(1)
```
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        vector<int> ans;
        for(int i=0;i<nums.size();i++){
              for(int j=i+1;j<nums.size();j++){
                  if(nums[i]+nums[j]==target){
                      ans.push_back(i);
                      ans.push_back(j);
                      return ans;
                  }
              }
        }
        return ans;
    }
};
```
 ### 排序+双指针法
  先将数组的顺序排好O(nlogn),再利用双指针法遍历一遍O(n)得到结果
  为保存下标信息另开一个数组
  时间复杂度O(nlogn),空间复杂度O(n)
```
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        vector<int> ans;
        vector<int> temp;
        temp=nums;
        int n=temp.size();
       sort(temp.begin(),temp.end());
       int i=0,j=n-1;
       while(i<j){
           if(temp[i]+temp[j]>target)j--;
          else if(temp[i]+temp[j]<target)i++;
          else break;
       }
       if(i<j){
      for(int k=0;k<n;k++){
          if(i<n&&nums[k]==temp[i]){
              ans.push_back(k);
              i=n;
          }
         else if(j<n&&nums[k]==temp[j]){
              ans.push_back(k);
              j=n;
          }
          if(i==n&&j==n)return ans;
      }
      }
        return ans;
    }
};
```
