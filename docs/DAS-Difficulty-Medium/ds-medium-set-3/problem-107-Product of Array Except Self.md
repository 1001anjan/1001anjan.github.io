---
layout: default
title: Product of Array Except Self
parent: Medium Set 3
grand_parent: DSA Medium
nav_order: 7
permalink: /problem-107-Product of Array Except Self/
---
# Product of Array Except Self
Given an integer array nums, return an array answer such that answer[i] is equal to the product of all the elements of nums except nums[i].

The product of any prefix or suffix of nums is guaranteed to fit in a 32-bit integer.

You must write an algorithm that runs in O(n) time and without using the division operation.

##### Example 1:
```markdown
Input: nums = [1,2,3,4]
Output: [24,12,8,6]
```
##### Example 2:
```markdown
Input: nums = [-1,1,0,-3,3]
Output: [0,0,9,0,0]
```
##### Constraints:
* 2 <= nums.length <= 10^5
* -30 <= nums[i] <= 30
* The product of any prefix or suffix of nums is guaranteed to fit in a 32-bit integer.

Follow up: Can you solve the problem in O(1) extra space complexity? (The output array does not count as extra space for space complexity analysis.)

### Solution:
```java
class Solution {
    public int[] productExceptSelf(int[] nums) {
        int pod = 1;
        int zero = 0;
        for(int n : nums){
            if(n == 0) zero++;
            else pod *= n;
            if(zero > 1) break;
        }
        if(zero > 1){
            for(int i = 0; i < nums.length; i++){
                nums[i] = 0;
            }
            return nums;
        }
        if(zero == 1){
            for(int i = 0; i < nums.length; i++){
                if(nums[i] == 0) nums[i] = pod;
                else nums[i] = 0;
            }
            return nums;
        }  
        
        for(int i = 0; i < nums.length; i++){
            nums[i] = pod / nums[i];
        }
        return nums;
    }
}
```