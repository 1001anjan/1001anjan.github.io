---
layout: default
title: Minimum Size Subarray Sum
parent: Data Structure Medium Set 2
grand_parent: Data Structure
nav_order: 48
permalink: /problem-98-Minimum Size Subarray Sum/
---
# Minimum Size Subarray Sum
Given an array of positive integers nums and a positive integer target, return the minimal length of a subarray whose sum is greater than or equal to target. If there is no such subarray, return 0 instead.

##### Example 1:
```markdown
Input: target = 7, nums = [2,3,1,2,4,3]
Output: 2
Explanation: The subarray [4,3] has the minimal length under the problem constraint.
```
##### Example 2:
```markdown
Input: target = 4, nums = [1,4,4]
Output: 1
```
##### Example 3:
```markdown
Input: target = 11, nums = [1,1,1,1,1,1,1,1]
Output: 0
```
##### Constraints:
* 1 <= target <= 10^9
* 1 <= nums.length <= 10^5
* 1 <= nums[i] <= 10^4


Follow up: If you have figured out the O(n) solution, try coding another solution of which the time complexity is O(n log(n)).

### Solution:
```java
class Solution {
    public int minSubArrayLen(int target, int[] nums) {
        int min = Integer.MAX_VALUE;
        int currSum = 0;
        int i = 0, j = 0;


        while(j < nums.length){
            currSum += nums[j];
            while(currSum >= target && i < nums.length){
                min = Math.min(min, j - i + 1);
                currSum -= nums[i++];
            }
            
            j++;
        }
        return min == Integer.MAX_VALUE? 0 : min;
    }
}
```