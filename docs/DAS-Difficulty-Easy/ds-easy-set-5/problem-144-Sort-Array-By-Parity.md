---
layout: default
title: Sort Array By Parity
parent: Easy Set 5
grand_parent: DSA Easy
nav_order: 14
permalink: /problem-144-Sort-Array-By-Parity/
---
# Sort Array By Parity

Given an integer array nums, move all the even integers at the beginning of the array followed by all the odd integers.

Return any array that satisfies this condition.

##### Example 1:
```markdown
Input: nums = [3,1,2,4]
Output: [2,4,3,1]
Explanation: The outputs [4,2,3,1], [2,4,1,3], and [4,2,1,3] would also be accepted.
```
##### Example 2:
```markdown
Input: nums = [0]
Output: [0]
```
##### Constraints:
* 1 <= nums.length <= 5000
* 0 <= nums[i] <= 5000

### Solution:
```java
class Solution {
    public int[] sortArrayByParity(int[] nums) {
        int s = 0;
        int e = nums.length - 1;
        while(s<e){
            // find odd number from left to right
            while(s<e && nums[s]%2 == 0) s++;
            // find even number from right to left
            while(s<e && nums[e]%2 != 0) e--;
            if(s<e){
                int t = nums[s];
                nums[s] = nums[e];
                nums[e] = t;
            }
        }
        return nums;
    }
}
```