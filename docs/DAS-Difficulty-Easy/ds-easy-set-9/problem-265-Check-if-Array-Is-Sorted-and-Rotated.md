---
layout: default
title: Check if Array Is Sorted and Rotated
parent: Easy Set 9
grand_parent: DSA Easy Difficulty
nav_order: 15
permalink: /problem-265-Check-if-Array-Is-Sorted-and-Rotated/
---
# Check if Array Is Sorted and Rotated
Given an array nums, return true if the array was originally sorted in non-decreasing order, then rotated some number of positions (including zero). Otherwise, return false.

There may be duplicates in the original array.

Note: An array A rotated by x positions results in an array B of the same length such that A[i] == B[(i+x) % A.length], where % is the modulo operation.

##### Example 1:
```markdown
Input: nums = [3,4,5,1,2]
Output: true
Explanation: [1,2,3,4,5] is the original sorted array.
You can rotate the array by x = 3 positions to begin on the the element of value 3: [3,4,5,1,2].
```
##### Example 2:
```markdown
Input: nums = [2,1,3,4]
Output: false
Explanation: There is no sorted array once rotated that can make nums.
```
##### Example 3:
```markdown
Input: nums = [1,2,3]
Output: true
Explanation: [1,2,3] is the original sorted array.
You can rotate the array by x = 0 positions (i.e. no rotation) to make nums.
```
##### Constraints:
* 1 <= nums.length <= 100
* 1 <= nums[i] <= 100

### Solution
```java
class Solution {
    public boolean check(int[] nums) {
        int i = 0;
        while(i < nums.length - 1 && nums[i] <= nums[i + 1]) i++;
        if(i == nums.length - 1) return true;
        // may have rotated array
        if(nums[0] < nums[nums.length - 1]) return false;
        i++;
        while(i < nums.length - 1 && nums[i] <= nums[i + 1]) i++;
        if(i == nums.length - 1) return true;
        
        return false;
        
    }
}
```