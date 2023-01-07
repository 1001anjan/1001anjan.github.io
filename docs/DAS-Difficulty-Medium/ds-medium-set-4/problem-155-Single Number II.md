---
layout: default
title: Single Number II
parent: Medium Set 4
grand_parent: DSA Medium Difficulty
nav_order: 5
permalink: /problem-155-Single Number II/
---
# Single Number II
Given an integer array nums where every element appears three times except for one, which appears exactly once. Find the single element and return it.

You must implement a solution with a linear runtime complexity and use only constant extra space.

##### Example 1:
```markdown
Input: nums = [2,2,3,2]
Output: 3
```
##### Example 2:
```markdown
Input: nums = [0,1,0,1,0,1,99]
Output: 99
```
##### Constraints:
* 1 <= nums.length <= 3 * 10^4
* -2^31 <= nums[i] <= 2^31 - 1
* Each element in nums appears exactly three times except for one element which appears once.

### Solution:
the number in 32 bits and just count how many 1s are there in each bit, and sum %= 3 will clear it once it reaches 3. After running for all the numbers for each bit, if we have a 1, then that 1 belongs to the single number, we can simply move it back to its spot by doing ans |= sum << i;

This has complexity of O(32n), which is essentially O(n) and very easy to think and implement. Plus, you get a general solution for any times of occurrence. Say all the numbers have 5 times, just do sum %= 5.
```java
class Solution {
    public int singleNumber(int[] nums) {
        int ans = 0;
        for(int i = 0; i < 32; i++){
            int sum = 0;
            for(int n : nums){
                if(((n >> i) & 1) == 1) sum++;
            }
            sum %= 3;
            ans = ans | sum << i;
        }

        return ans;
    }
}
```