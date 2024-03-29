---
layout: default
title: Binary Prefix Divisible By 5
parent: Easy Set 6
grand_parent: DSA Easy
nav_order: 4
permalink: /problem-164-Binary-Prefix-Divisible-By-5/
---
# Binary Prefix Divisible By 5
You are given a binary array nums (0-indexed).

We define xi as the number whose binary representation is the subarray nums[0..i] (from most-significant-bit to least-significant-bit).

* For example, if nums = [1,0,1], then x0 = 1, x1 = 2, and x2 = 5.
Return an array of booleans answer where answer[i] is true if xi is divisible by 5.

##### Example 1:
```markdown
Input: nums = [0,1,1]
Output: [true,false,false]
Explanation: The input numbers in binary are 0, 01, 011; which are 0, 1, and 3 in base-10.
Only the first number is divisible by 5, so answer[0] is true.
```
##### Example 2:
```markdown
Input: nums = [1,1,1]
Output: [false,false,false]
```
##### Constraints:
* 1 <= nums.length <= 105
* nums[i] is either 0 or 1.

### Solution:
```java
class Solution {
    public List<Boolean> prefixesDivBy5(int[] nums) {
        List<Boolean> ans = new LinkedList<>();
        long n = 0;
        for(int i=0; i<nums.length; i++)
            ans.add((n = (n << 1 | nums[i]) % 5) == 0);
        return ans;
    }
}
```