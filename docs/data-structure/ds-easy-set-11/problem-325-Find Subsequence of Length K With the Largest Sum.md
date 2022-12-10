---
layout: default
title: Find Subsequence of Length K With the Largest Sum
parent: Data Structure Easy Set 11
grand_parent: Data Structure
nav_order: 15
permalink: /problem-325-Find Subsequence of Length K With the Largest Sum/
---
# Find Subsequence of Length K With the Largest Sum

You are given an integer array nums and an integer k. You want to find a subsequence of nums of length k that has the largest sum.

Return any such subsequence as an integer array of length k.

A subsequence is an array that can be derived from another array by deleting some or no elements without changing the order of the remaining elements.

##### Example 1:
```markdown
Input: nums = [2,1,3,3], k = 2
Output: [3,3]
Explanation:
The subsequence has the largest sum of 3 + 3 = 6.
```
##### Example 2:
```markdown
Input: nums = [-1,-2,3,4], k = 3
Output: [-1,3,4]
Explanation:
The subsequence has the largest sum of -1 + 3 + 4 = 6.
```
##### Example 3:
```markdown
Input: nums = [3,4,3,3], k = 2
Output: [3,4]
Explanation:
The subsequence has the largest sum of 3 + 4 = 7.
Another possible subsequence is [4, 3].
```
##### Constraints:
* 1 <= nums.length <= 1000
* -105 <= nums[i] <= 105
* 1 <= k <= nums.length

### Solution:
```java
class Solution {
    public int[] maxSubsequence(int[] nums, int k) {
        int[][] dp = new int[nums.length][2];
        for(int i =0; i < nums.length; i++){
            dp[i][0] = nums[i];
            dp[i][1] = i;
        }
        
        Arrays.sort(dp,(a,b) -> a[0] - b[0]);
        int[][] sortedSeq = new int[k][2];
        int m = k - 1;
        for(int i = nums.length - 1; i >= nums.length - k; i--, m--){
            sortedSeq[m][0] = dp[i][0];
            sortedSeq[m][1] = dp[i][1];
        }
        
        Arrays.sort(sortedSeq, (a,b) -> a[1] - b[1]);
        int[] ans = new int[k];
        for(int i = 0; i < k; i++){
            ans[i] = sortedSeq[i][0];
        }
        return ans;
    }
}
```