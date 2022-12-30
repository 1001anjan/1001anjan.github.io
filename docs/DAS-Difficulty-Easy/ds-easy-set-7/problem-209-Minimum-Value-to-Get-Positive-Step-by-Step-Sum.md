---
layout: default
title: Minimum Value to Get Positive Step by Step Sum
parent: Easy Set 7
grand_parent: DSA Easy Difficulty
nav_order: 19
permalink: /problem-209-Minimum-Value-to-Get-Positive-Step-by-Step-Sum/
---
# Minimum Value to Get Positive Step by Step Sum
Given an array of integers nums, you start with an initial positive value startValue.

In each iteration, you calculate the step by step sum of startValue plus elements in nums (from left to right).

Return the minimum positive value of startValue such that the step by step sum is never less than 1.

##### Example 1:
```markdown
Input: nums = [-3,2,-3,4,2]
Output: 5
Explanation: If you choose startValue = 4, in the third iteration your step by step sum is less than 1.
step by step sum
startValue = 4 | startValue = 5 | nums
(4 -3 ) = 1  | (5 -3 ) = 2    |  -3
(1 +2 ) = 3  | (2 +2 ) = 4    |   2
(3 -3 ) = 0  | (4 -3 ) = 1    |  -3
(0 +4 ) = 4  | (1 +4 ) = 5    |   4
(4 +2 ) = 6  | (5 +2 ) = 7    |   2
```
##### Example 2:
```markdown
Input: nums = [1,2]
Output: 1
Explanation: Minimum start value should be positive.
```
##### Example 3:
```markdown
Input: nums = [1,-2,-3]
Output: 5
```
##### Constraints:
* 1 <= nums.length <= 100
* -100 <= nums[i] <= 100

### Solution:
```java
class Solution {
    public int minStartValue(int[] nums) {
        int start = nums[0];
        if(start < 0) 
            start = (start*-1) + 1;
        else start = 1;
        int i = 0;
        while(i != nums.length){
            int temp = start;
            for(i = 0; i < nums.length; i++){
                temp = temp + nums[i];
                if(temp < 1){
                    start++;
                    break;
                }
            }
        }
        return start;
    }
}
```
#### Faster Solution
```java
class Solution {
    public int minStartValue(int[] nums) {
        int preSum=0;
        int minSum=Integer.MAX_VALUE;
        
        for(int i : nums){
            preSum+=i;
            
            minSum=Math.min(minSum,preSum);
        }
        
        return minSum > 0 ? 1 : Math.abs(minSum) + 1;
    }
}
```