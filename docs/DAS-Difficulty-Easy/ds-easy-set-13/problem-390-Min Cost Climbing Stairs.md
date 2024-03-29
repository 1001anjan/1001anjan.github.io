---
layout: default
title: Min Cost Climbing Stairs
parent: Easy Set 13
grand_parent: DSA Easy
nav_order: 20
permalink: /problem-390-Min Cost Climbing Stairs/
---
# Min Cost Climbing Stairs
You are given an integer array cost where cost[i] is the cost of ith step on a staircase. Once you pay the cost, you can either climb one or two steps.

You can either start from the step with index 0, or the step with index 1.

Return the minimum cost to reach the top of the floor.

##### Example 1:
```markdown
Input: cost = [10,15,20]
Output: 15
Explanation: You will start at index 1.
- Pay 15 and climb two steps to reach the top.
  The total cost is 15.
```
##### Example 2:
```markdown
Input: cost = [1,100,1,1,1,100,1,1,100,1]
Output: 6
Explanation: You will start at index 0.
- Pay 1 and climb two steps to reach index 2.
- Pay 1 and climb two steps to reach index 4.
- Pay 1 and climb two steps to reach index 6.
- Pay 1 and climb one step to reach index 7.
- Pay 1 and climb two steps to reach index 9.
- Pay 1 and climb one step to reach the top.
  The total cost is 6.
```
##### Constraints:
* 2 <= cost.length <= 1000
* 0 <= cost[i] <= 999

### Solution:
```java
class Solution {
    public int minCostClimbingStairs(int[] cost) {
        int[] dp = new int[cost.length + 2];
        for(int i = cost.length - 1; i >= 0; i--){
            dp[i] = cost[i] + Math.min(dp[i + 1], dp[i + 2]);
        }
        return Math.min(dp[0],dp[1]);
    } 
}
```