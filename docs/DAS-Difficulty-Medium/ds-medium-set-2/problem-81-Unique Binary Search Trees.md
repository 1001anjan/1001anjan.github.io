---
layout: default
title: Unique Binary Search Trees
parent: Medium Set 2
grand_parent: DSA Medium Difficulty
nav_order: 31
permalink: /problem-81-Unique Binary Search Trees/
---
# Unique Binary Search Trees
Given an integer n, return the number of structurally unique BST's (binary search trees) which has exactly n nodes of unique values from 1 to n.

##### Example 1:
![](../../assets/images/ds/uniquebstn3.jpeg)
```markdown
Input: n = 3
Output: 5
```
##### Example 2:
```markdown
Input: n = 1
Output: 1
```
##### Constraints:
* 1 <= n <= 19

### Solution:
```java
class Solution {
    public int numTrees(int n) {
        int[] dp = new int[n + 1];
        dp[0] = 1;
        dp[1] = 1;

        for(int i = 2; i <= n; i++){
            for(int j = 1; j <= i; j++){
                dp[i] += dp[j - 1] * dp[i - j];
            }
        }

        return dp[n];
    }
}
```