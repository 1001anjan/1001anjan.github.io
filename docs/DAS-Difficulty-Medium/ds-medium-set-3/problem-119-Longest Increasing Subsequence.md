---
layout: default
title: Longest Increasing Subsequence
parent: Medium Set 3
grand_parent: DSA Medium Difficulty
nav_order: 19
permalink: /problem-119-Longest Increasing Subsequence/
---
# Longest Increasing Subsequence
Given an integer array nums, return the length of the longest strictly increasing subsequence.

##### Example 1:
```markdown
Input: nums = [10,9,2,5,3,7,101,18]
Output: 4
Explanation: The longest increasing subsequence is [2,3,7,101], therefore the length is 4.
```
##### Example 2:
```markdown
Input: nums = [0,1,0,3,2,3]
Output: 4
```
##### Example 3:
```markdown
Input: nums = [7,7,7,7,7,7,7]
Output: 1
```
##### Constraints:
* 1 <= nums.length <= 2500
* -10^4 <= nums[i] <= 10^4

* Follow up: Can you come up with an algorithm that runs in O(n log(n)) time complexity?

### Solution:
```java
class Solution {
    public int lengthOfLIS(int[] nums) {
        int[] dp = new int[nums.length];
        int len = 0;
        for(int n : nums){
            int i = Arrays.binarySearch(dp, 0, len, n);
            if(i < 0) i = -(i + 1);
            dp[i] = n;
            if(i == len) len ++;
        }

        return len;
    }
}
```