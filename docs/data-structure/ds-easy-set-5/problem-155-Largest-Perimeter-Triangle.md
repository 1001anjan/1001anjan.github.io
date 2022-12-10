---
layout: default
title: Largest Perimeter Triangle
parent: Data Structure Easy Set 5
grand_parent: Data Structure
nav_order: 25
permalink: /problem-155-Largest-Perimeter-Triangle/
---
# Largest Perimeter Triangle
Given an integer array nums, return the largest perimeter of a triangle with a non-zero area, formed from three of these lengths. If it is impossible to form any triangle of a non-zero area, return 0.

##### Example 1:
```markdown
Input: nums = [2,1,2]
Output: 5
```
##### Example 2:
```markdown
Input: nums = [1,2,1]
Output: 0
```
##### Constraints:
* 3 <= nums.length <= 104
* 1 <= nums[i] <= 106

### Solution:
```java
class Solution {
    public int largestPerimeter(int[] nums) {
        Arrays.sort(nums);
        for(int i=nums.length-3; i>=0; i--){
            if(nums[i] + nums[i+1] > nums[i+2]) return nums[i] + nums[i+1] + nums[i+2];
        }
        return 0;
    }
}
```