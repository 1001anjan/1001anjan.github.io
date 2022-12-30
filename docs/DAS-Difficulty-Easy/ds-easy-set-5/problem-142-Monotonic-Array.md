---
layout: default
title:  Monotonic Array
parent: Easy Set 5
grand_parent: DSA Easy Difficulty
nav_order: 12
permalink: /problem-142-Monotonic-Array/
---
# Monotonic Array

An array is monotonic if it is either monotone increasing or monotone decreasing.

An array nums is monotone increasing if for all i <= j, nums[i] <= nums[j]. An array nums is monotone decreasing if for all i <= j, nums[i] >= nums[j].

Given an integer array nums, return true if the given array is monotonic, or false otherwise.

##### Example 1:
```markdown
Input: nums = [1,2,2,3]
Output: true
```
##### Example 2:
```markdown
Input: nums = [6,5,4,4]
Output: true
```
##### Example 3:
```markdown
Input: nums = [1,3,2]
Output: false
```
##### Constraints:
* 1 <= nums.length <= 105
* -105 <= nums[i] <= 105

### Solution:
```java
class Solution {
    public boolean isMonotonic(int[] nums) {
       if(nums[0]<=nums[nums.length-1]){
          for(int i=1; i<nums.length; i++){
              if(nums[i-1]>nums[i]) return false;
          } 
       }else{
           for(int i=1; i<nums.length; i++){
              if(nums[i-1]<nums[i]) return false;
          } 
       }
        return true;
    }
}
```