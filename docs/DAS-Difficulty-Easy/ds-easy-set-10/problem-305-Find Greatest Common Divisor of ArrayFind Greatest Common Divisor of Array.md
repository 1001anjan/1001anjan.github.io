---
layout: default
title: Find Greatest Common Divisor of Array
parent: Easy Set 10
grand_parent: DSA Easy Difficulty
nav_order: 25
permalink: /problem-305-Find Greatest Common Divisor of Array/
---
# Find Greatest Common Divisor of Array

Given an integer array nums, return the greatest common divisor of the smallest number and largest number in nums.

The greatest common divisor of two numbers is the largest positive integer that evenly divides both numbers.

##### Example 1:
```markdown
Input: nums = [2,5,6,9,10]
Output: 2
Explanation:
The smallest number in nums is 2.
The largest number in nums is 10.
The greatest common divisor of 2 and 10 is 2.
```
##### Example 2:
```markdown
Input: nums = [7,5,6,8,3]
Output: 1
Explanation:
The smallest number in nums is 3.
The largest number in nums is 8.
The greatest common divisor of 3 and 8 is 1.
```
##### Example 3:
```markdown
Input: nums = [3,3]
Output: 3
Explanation:
The smallest number in nums is 3.
The largest number in nums is 3.
The greatest common divisor of 3 and 3 is 3.
```
##### Constraints:
* 2 <= nums.length <= 1000
* 1 <= nums[i] <= 1000

### Solution:
```java
class Solution {
    public int findGCD(int[] nums) {
        int mx, mn;
        mx = mn = nums[0];
        for(int n : nums){
            if(n > mx) mx = n;
            if(n < mn) mn = n;
        }
        
        for(int i = mn; i >= 1; i--){
            if(mx % i == 0 && mn % i == 0) return i;
        }
        
        throw null;
    }
}
```