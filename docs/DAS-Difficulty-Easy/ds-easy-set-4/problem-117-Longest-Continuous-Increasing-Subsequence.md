---
layout: default
title: Longest Continuous Increasing Subsequence
parent: Easy Set 4
grand_parent: DSA Easy
nav_order: 17
permalink: /problem-117-Longest-Continuous-Increasing-Subsequence/
---
# Longest Continuous Increasing Subsequence

Given an unsorted array of integers nums, return the length of the longest continuous increasing subsequence (i.e. subarray). The subsequence must be strictly increasing.

A continuous increasing subsequence is defined by two indices l and r (l < r) such that it is [nums[l], nums[l + 1], ..., nums[r - 1], nums[r]] and for each l <= i < r, nums[i] < nums[i + 1].

##### Example 1:
```markdown
Input: nums = [1,3,5,4,7]
Output: 3
Explanation: The longest continuous increasing subsequence is [1,3,5] with length 3.
Even though [1,3,5,7] is an increasing subsequence, it is not continuous as elements 5 and 7 are separated by element 4.
```

##### Example 2:
```markdown
Input: nums = [2,2,2,2,2]
Output: 1
Explanation: The longest continuous increasing subsequence is [2] with length 1. Note that it must be strictly
increasing.
```

##### Constraints:
* 1 <= nums.length <= 104
* -109 <= nums[i] <= 109

### Solution:
```java
class Solution {
    public int findLengthOfLCIS(int[] nums) {
        int currCount = 1;
        int prevCount = 1;
        for(int i=1; i<nums.length; i++){
            if(nums[i-1]<nums[i]) currCount++;
            else{
                prevCount = Math.max(prevCount, currCount);
                currCount = 1;
            }
        }
        return Math.max(prevCount, currCount);
    }
}
```