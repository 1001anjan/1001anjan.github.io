---
layout: default
title: Sort Array By Parity II
parent: Easy Set 5
grand_parent: DSA Easy
nav_order: 16
permalink: /problem-146-Sort-Array-By-Parity-II/
---
# Sort Array By Parity II

Given an array of integers nums, half of the integers in nums are odd, and the other half are even.

Sort the array so that whenever nums[i] is odd, i is odd, and whenever nums[i] is even, i is even.

Return any answer array that satisfies this condition.

##### Example 1:
```markdown
Input: nums = [4,2,5,7]
Output: [4,5,2,7]
Explanation: [4,7,2,5], [2,5,4,7], [2,7,4,5] would also have been accepted.
```
##### Example 2:
```markdown
Input: nums = [2,3]
Output: [2,3]
```
##### Constraints:
* 2 <= nums.length <= 2 * 104
* nums.length is even.
* Half of the integers in nums are even.
* 0 <= nums[i] <= 1000

### Solution:
```java
class Solution {
    public int[] sortArrayByParityII(int[] nums) {
        int e = 0;
        int o = 1;
        while(e<nums.length){
            while(e<nums.length && nums[e]%2 == 0) e += 2;
            while(o<nums.length && nums[o]%2 != 0) o += 2;
            if(e<nums.length && o<nums.length){
                int t = nums[e];
                nums[e] = nums[o];
                nums[o] = t;
            }
            e += 2;
            o += 2;
        }
        return nums;
    }
}
```