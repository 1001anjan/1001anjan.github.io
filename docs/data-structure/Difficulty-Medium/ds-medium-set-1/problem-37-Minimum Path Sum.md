---
layout: default
title: Minimum Path Sum
parent: Data Structure Medium Set 1
grand_parent: Data Structure
nav_order: 37
permalink: /problem-37-Minimum Path Sum/
---
# Minimum Path Sum
Given a m x n grid filled with non-negative numbers, find a path from top left to bottom right, which minimizes the sum of all numbers along its path.

Note: You can only move either down or right at any point in time.

##### Example 1:

```markdown
Input: grid = [[1,3,1],[1,5,1],[4,2,1]]
Output: 7
Explanation: Because the path 1 → 3 → 1 → 1 → 1 minimizes the sum.
```
##### Example 2:
```markdown
Input: grid = [[1,2,3],[4,5,6]]
Output: 12
```
##### Constraints:
* m == grid.length
* n == grid[i].length
* 1 <= m, n <= 200
* 0 <= grid[i][j] <= 100

### Solution:
```java
class Solution {
    public int minPathSum(int[][] grid) {
        int m = grid.length;
        int n = grid[0].length;
        int[][] dp = new int[m][n];

        int sum = 0;
        for(int i = 0; i < n; i++){
            sum = sum + grid[0][i];
            dp[0][i] = sum;
        } 

        sum = 0;
        for(int i = 0; i < m; i++){
            sum += grid[i][0];
            dp[i][0] = sum;
        }

        for(int i = 1; i < m; i++){
            for(int j = 1; j < n; j++){
                dp[i][j] = Math.min(grid[i][j] + dp[i - 1][j], grid[i][j] + dp[i][j - 1]);
            }
        }

        return dp[m - 1][n - 1];
    }
}
```