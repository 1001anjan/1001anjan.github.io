---
layout: default
title: Subarray Sums Divisible by K
parent: Medium Set 4
grand_parent: DSA Medium
nav_order: 18
permalink: /problem-168-Subarray Sums Divisible by K/
---
# Subarray Sums Divisible by K
Given an integer array nums and an integer k, return the number of non-empty subarrays that have a sum divisible by k.

A subarray is a contiguous part of an array.

##### Example 1:
```markdown
Input: nums = [4,5,0,-2,-3,1], k = 5
Output: 7
Explanation: There are 7 subarrays with a sum divisible by k = 5:
[4, 5, 0, -2, -3, 1], [5], [5, 0], [5, 0, -2, -3], [0], [0, -2, -3], [-2, -3]
```
##### Example 2:
```markdown
Input: nums = [5], k = 9
Output: 0
```
##### Constraints:
* 1 <= nums.length <= 3 * 10^4
* -10^4 <= nums[i] <= 10^4
* 2 <= k <= 10^4

### Solution:
##### Time Limit Exceeded. Time Complexity O(n^2), Space Complexity: O(n)
```java
class Solution {
    public int subarraysDivByK(int[] nums, int k) {
        int[] dp = new int[nums.length + 1];
        int sum = 0;
        dp[0] = 0;
        for(int i = 0; i < nums.length; i++){
            sum += nums[i];
            dp[i + 1] = sum;
        }

        //
        int count = 0;
        for(int i = 0; i < dp.length; i++){
            for(int j = i + 1; j < dp.length; j++){
                if((dp[j] - dp[i]) % k == 0) count++;
            }
        }
        return count;
    }

}
```
##### Improvement
when (dp[j] - dp[i]) % k = 0 means dp[j] % k = dp[i] % k 
here dp[i] means prefix sum 0 to i.
```java
class Solution {
    public int subarraysDivByK(int[] nums, int k) {
        // There are k mod groups 0...k-1.
        int[] reminder = new int[k];
        int prefixSum = 0;
        reminder[0] = 1;
        int count = 0;
        for(int n : nums){
            prefixSum += n;
            // Take modulo twice to avoid negative remainders.
            int r = (prefixSum % k + k) % k;
            count += reminder[r];
            reminder[r] ++;
        }
        return count;
    }
}
```