---
layout: default
title: Single Number
parent: Easy Set 1
grand_parent: DSA Easy Difficulty
nav_order: 29
permalink: /problem-29-Single-Number/
---
# Single Number
Given a non-empty array of integers nums, every element appears twice except for one. Find that single one.

You must implement a solution with a linear runtime complexity and use only constant extra space.

##### Example 1:
```markdown
Input: nums = [2,2,1]
Output: 1
```
##### Example 2:
```markdown
Input: nums = [4,1,2,1,2]
Output: 4
```
##### Example 3:
```markdown
Input: nums = [1]
Output: 1
```

##### Constraints:

* 1 <= nums.length <= 3 * 104
* -3 * 104 <= nums[i] <= 3 * 104
* Each element in the array appears twice except for one element which appears only once.

### Solution
#### XOR
```java
class Solution {
    public int singleNumber(int[] nums) {
        int x = nums[0];
        for(int i=1; i<nums.length; i++){
            x = x^nums[i];
        }
        return x;
    }
}
```

