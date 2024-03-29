---
layout: default
title: Maximum Subarray
parent: Easy Set 1
grand_parent: DSA Easy
nav_order: 11
permalink: /problem-11-maximum-subarray/
---
# Maximum Subarray

Given an integer array nums, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.

A subarray is a contiguous part of an array.

#### Example 1:
```markdown
Input: nums = [-2,1,-3,4,-1,2,1,-5,4]
Output: 6
Explanation: [4,-1,2,1] has the largest sum = 6.
```
#### Example 2:
```markdown
Input: nums = [1]
Output: 1
```
#### Example 3:
```markdown
Input: nums = [5,4,-1,7,8]
Output: 23
```

### Constraints:
* 1 <= nums.length <= 105
* -104 <= nums[i] <= 104


Follow up: If you have figured out the O(n) solution, try coding another solution using the divide and conquer approach, which is more subtle.
```java
class Solution {
    public int maxSubArray(int[] nums) {
        int prevSum    = nums[0];
        int currentSum = nums[0];
        for(int i = 1; i < nums.length; i++){
            if(currentSum + nums[i]< nums[i]){
                currentSum = nums[i];
            }else{
                currentSum += nums[i];
            }
            prevSum = Math.max(prevSum, currentSum);
        }
        return Math.max(prevSum, currentSum);
    }
}
```
