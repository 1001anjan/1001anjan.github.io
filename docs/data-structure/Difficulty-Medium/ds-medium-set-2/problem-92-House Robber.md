---
layout: default
title: House Robber
parent: Data Structure Medium Set 2
grand_parent: Data Structure
nav_order: 42
permalink: /problem-92-House Robber/
---
# House Robber
You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security systems connected and it will automatically contact the police if two adjacent houses were broken into on the same night.

Given an integer array nums representing the amount of money of each house, return the maximum amount of money you can rob tonight without alerting the police.

##### Example 1:
```markdown
Input: nums = [1,2,3,1]
Output: 4
Explanation: Rob house 1 (money = 1) and then rob house 3 (money = 3).
Total amount you can rob = 1 + 3 = 4.
```
##### Example 2:
```markdown
Input: nums = [2,7,9,3,1]
Output: 12
Explanation: Rob house 1 (money = 2), rob house 3 (money = 9) and rob house 5 (money = 1).
Total amount you can rob = 2 + 9 + 1 = 12.
```
##### Constraints:
* 1 <= nums.length <= 100
* 0 <= nums[i] <= 400

### Solution:
```java
class Solution {
    public int rob(int[] nums) {
        int[][] dp = new int[nums.length + 1][2];
        // dp[i][0] means if we dont rob ithe house and dp[i][1] if we rob ith house 
        for(int i = 1; i <= nums.length; i++){
            dp[i][0] = Math.max(dp[i - 1][0], dp[i - 1][1]);
            dp[i][1] = nums[i - 1] + dp[i - 1][0];
        }

        return Math.max(dp[nums.length][0], dp[nums.length][1]);
    }
}
```
##### Converting the solution to O(1) space
```java
class Solution {
    public int rob(int[] nums) {
        int prevNo = 0; // the max value if previous hous is not robbed 
        int prevYes = 0; // the max value if previous hous is robbed 
        for(int n : nums){
           int temp = prevNo;
           prevNo = Math.max(prevNo, prevYes);
           prevYes = temp + n;
        }

        return Math.max(prevNo, prevYes);
    }
}
```

