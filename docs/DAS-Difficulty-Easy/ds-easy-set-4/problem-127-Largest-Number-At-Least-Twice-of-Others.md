---
layout: default
title: Largest Number At Least Twice of Others
parent: Easy Set 4
grand_parent: DSA Easy Difficulty
nav_order: 27
permalink: /problem-127-Largest-Number-At-Least-Twice-of-Others/
---
# Largest Number At Least Twice of Others
You are given an integer array nums where the largest integer is unique.

Determine whether the largest element in the array is at least twice as much as every other number in the array. If it is, return the index of the largest element, or return -1 otherwise.

##### Example 1:
```markdown
Input: nums = [3,6,1,0]
Output: 1
Explanation: 6 is the largest integer.
For every other number in the array x, 6 is at least twice as big as x.
The index of value 6 is 1, so we return 1.
```
##### Example 2:
```markdown
Input: nums = [1,2,3,4]
Output: -1
Explanation: 4 is less than twice the value of 3, so we return -1.
```
##### Constraints:
* 1 <= nums.length <= 50
* 0 <= nums[i] <= 100
* The largest element in nums is unique.

### Solution:
```java
class Solution {
    public int dominantIndex(int[] nums) {
        int max = nums[0];
        int index = 0;
        for(int i =0; i<nums.length; i++){
            if(max<nums[i]) {
                max = nums[i];
                index = i;
            }
        } 
        for(int i=0; i<nums.length; i++){
            if(i != index && max<nums[i]*2) return -1;
        }
        return index;
    }
}
```
