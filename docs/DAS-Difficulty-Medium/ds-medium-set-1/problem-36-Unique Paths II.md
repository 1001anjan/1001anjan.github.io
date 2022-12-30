---
layout: default
title: Unique Paths II
parent: Medium Set 1
grand_parent: DSA Medium Difficulty
nav_order: 36
permalink: /problem-36-Unique Paths II/
---

# Unique Paths II
You are given an m x n integer array grid. There is a robot initially located at the top-left corner (i.e., grid[0][0]). The robot tries to move to the bottom-right corner (i.e., grid[m - 1][n - 1]). The robot can only move either down or right at any point in time.

An obstacle and space are marked as 1 or 0 respectively in grid. A path that the robot takes cannot include any square that is an obstacle.

Return the number of possible unique paths that the robot can take to reach the bottom-right corner.

The testcases are generated so that the answer will be less than or equal to 2 * 109.

##### Example 1:
![](../../assets/images/ds/robot1.jpeg)
```markdown
Input: obstacleGrid = [[0,0,0],[0,1,0],[0,0,0]]
Output: 2
Explanation: There is one obstacle in the middle of the 3x3 grid above.
There are two ways to reach the bottom-right corner:
1. Right -> Right -> Down -> Down
2. Down -> Down -> Right -> Right
```
##### Example 2:
![](../../assets/images/ds/robot2.jpeg)
```markdown
Input: obstacleGrid = [[0,1],[0,0]]
Output: 1
```
##### Constraints:
* m == obstacleGrid.length
* n == obstacleGrid[i].length
* 1 <= m, n <= 100
* obstacleGrid[i][j] is 0 or 1.

### Solution: 
##### Time Limit Exceeded

```java
class Solution {
    public int uniquePathsWithObstacles(int[][] obstacleGrid) {
                
        if(obstacleGrid.length == 0 || obstacleGrid[0].length == 0 || obstacleGrid[0][0] ==  1) {
            return 0;
        }
        return paths(obstacleGrid, obstacleGrid.length-1, obstacleGrid[0].length-1);
        
    }
    
    private int paths(int[][] obstacleGrid, int m, int n){
        
        if(m == 0 && n == 0) return 1;
        
        if(m<0 || n<0 || obstacleGrid[m][n] == 1) return 0;
        
        return paths(obstacleGrid, m-1,n)+paths(obstacleGrid, m,n-1);
        
    }
}
```
##### With memorization 
```java
class Solution {
    public int uniquePathsWithObstacles(int[][] obstacleGrid) {
        Map<String,Integer> dp = new HashMap<>();    
        if(obstacleGrid.length == 0 || obstacleGrid[0].length == 0 || obstacleGrid[0][0] ==  1) {
            return 0;
        }
        return paths(obstacleGrid, obstacleGrid.length-1, obstacleGrid[0].length-1, dp);
        
    }
    
    private int paths(int[][] obstacleGrid, int m, int n, Map<String,Integer> dp){
        String key = m+"-"+n;
        if(m == 0 && n == 0) return 1;
        
        if(m<0 || n<0 || obstacleGrid[m][n] == 1) return 0;
        if(dp.containsKey(key)) return dp.get(key);
        dp.put(key, paths(obstacleGrid, m-1,n, dp)+paths(obstacleGrid, m,n-1, dp));
        return dp.get(key);
    }
}
```
##### Dynamic programming 
```java
class Solution {
    public int uniquePathsWithObstacles(int[][] obstacleGrid) {
        int m = obstacleGrid.length;
        int n = obstacleGrid[0].length;

        int[][] dp = new int[m][n];

        // intializing base dp
        boolean found = false;
        
        for(int i = 0; i < m ; i++){
            if(obstacleGrid[i][0] == 1) found = true;
            if(!found) dp[i][0] = 1;
            else dp[i][0] = 0;
        }
        found = false;
        for(int i = 0; i < n ; i++){
            if(obstacleGrid[0][i] == 1) found = true;
            if(!found) dp[0][i] = 1;
            else dp[0][i] = 0;
        }

        // process the paths
        for(int i = 1; i < m; i++){
            for(int j = 1; j < n; j++){
                if(obstacleGrid[i][j] == 1){
                    dp[i][j] = 0;
                }else{
                    dp[i][j] = dp[i - 1][j] + dp[i][j - 1];
                }
            }
        }
        
        return dp[m - 1][n - 1];
    }
}
```
```java
class Solution {
    public int uniquePathsWithObstacles(int[][] obstacleGrid) {
        int width = obstacleGrid[0].length;
        int[] dp = new int[width];
        dp[0] = 1;
        for (int[] row : obstacleGrid) {
            for (int j = 0; j < width; j++) {
                if (row[j] == 1)
                    dp[j] = 0;
                else if (j > 0)
                    dp[j] += dp[j - 1];
            }
        }
        return dp[width - 1];
    }
}
```