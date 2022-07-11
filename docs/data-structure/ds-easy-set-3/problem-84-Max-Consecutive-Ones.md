---
layout: default
title: Max Consecutive Ones
parent: Data Structure Easy Set 3
grand_parent: Data Structure
nav_order: 21
permalink: /problem-84-Max-Consecutive-Ones/
---
# Max Consecutive Ones

Given a binary array nums, return the maximum number of consecutive 1's in the array.

##### Example 1:
```markdown
Input: nums = [1,1,0,1,1,1]
Output: 3
Explanation: The first two digits or the last three digits are consecutive 1s. The maximum number of consecutive 1s is 3.
```
##### Example 2:
```markdown
Input: nums = [1,0,1,1,0,1]
Output: 2
```
##### Constraints:
* 1 <= nums.length <= 105
* nums[i] is either 0 or 1.

### Solution
```java
class Solution {
    public int findMaxConsecutiveOnes(int[] nums) {
        int m = 0;
        int p = 0;
        int i = 0;
        while(i<nums.length){
            if(nums[i] == 0) {
                i++;
                continue;
            }
            while(i<nums.length && nums[i] == 1){
                m++;
                i++;
            }
            if(m>p){
                p = m;
            }
            m = 0;
        }
        return p;
    }
}
```