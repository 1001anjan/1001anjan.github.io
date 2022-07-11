---
layout: default
title: Climbing Stairs
parent: Data Structure Easy Set 1
grand_parent: Data Structure
nav_order: 16
permalink: /problem-16-climbing-stairs/
---
# Climbing Stairs

You are climbing a staircase. It takes n steps to reach the top.

Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

#### Example 1:
```markdown
Input: n = 2
Output: 2
Explanation: There are two ways to climb to the top.
1. 1 step + 1 step
2. 2 steps
```

#### Example 2:
```markdown
Input: n = 3
Output: 3
Explanation: There are three ways to climb to the top.
1. 1 step + 1 step + 1 step
2. 1 step + 2 steps
3. 2 steps + 1 step
```
### Constraints:

* 1 <= n <= 45

### Solution
```java
class Solution {
    public int climbStairs(int n) {
        if(n <= 2)
            return n;
        int[] dp = new int[n+1];
        dp[1] = 1;
        dp[2] = 2;
        for(int i = 3; i <= n; i++)
            dp[i] = dp[i-1] + dp[i-2];
        return dp[n];
    }
}
```
### Recursion 
```java
class Solution {
    HashMap<Integer, Integer> map = new HashMap();
    public int climbStairs(int n) {
        if(map.containsKey(n)) return map.get(n);
        if(n == 1){
            map.put(1, 1);
            return 1;
        } 
        if(n == 2) {
            map.put(2, 2);
            return 2;
        }
        int x =  climbStairs(n-1) + climbStairs(n-2);
        map.put(n,x);
        return map.get(n);
    }
}
```