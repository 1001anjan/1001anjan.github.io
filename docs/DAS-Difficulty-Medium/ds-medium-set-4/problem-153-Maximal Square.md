---
layout: default
title: Maximal Square
parent: Medium Set 4
grand_parent: DSA Medium Difficulty
nav_order: 3
permalink: /problem-153-Maximal Square/
---
# Maximal Square
Given an m x n binary matrix filled with 0's and 1's, find the largest square containing only 1's and return its area.

##### Example 1:
![](../../assets/images/ds/max1grid.jpeg)
```markdown
Input: matrix = [["1","0","1","0","0"],["1","0","1","1","1"],["1","1","1","1","1"],["1","0","0","1","0"]]
Output: 4
```
##### Example 2:
![](../../assets/images/ds/max2grid.jpeg)
```markdown
Input: matrix = [["0","1"],["1","0"]]
Output: 1
```
##### Example 3:
```markdown
Input: matrix = [["0"]]
Output: 0
```
##### Constraints:
* m == matrix.length
* n == matrix[i].length
* 1 <= m, n <= 300
* matrix[i][j] is '0' or '1'.

### Solution:
```java
class Solution {
    public int maximalSquare(char[][] matrix) {
       int m = matrix.length, n = matrix[0].length;

       int[][] dp = new int[m + 1][n + 1];
        int maxLen = 0;
       for(int i = 1; i <= m; i++){
           for(int j = 1; j <=n; j++){
               if(matrix[i - 1][j - 1] == '1'){
                   dp[i][j] = 1 + Math.min(dp[i][j - 1], Math.min(dp[i - 1][j - 1], dp[i - 1][j]));
                   maxLen = Math.max(maxLen, dp[i][j]);
               }
           }
       }

       return maxLen * maxLen;
    }
}
```
##### (Better Dynamic Programming)
#### Algorithm
![](../../assets/images/ds/221_Maximal_Square1.png)
```java
class Solution {
    public int maximalSquare(char[][] matrix) {
       int m = matrix.length, n = matrix[0].length;

       int[] dp = new int[n + 1];
        int maxLen = 0, prev = 0;
       for(int i = 1; i <= m; i++){
           for(int j = 1; j <= n; j++){
               int temp = dp[j];
               if(matrix[i - 1][j - 1] == '1'){
                   dp[j] = 1 + Math.min(dp[j - 1], Math.min(prev, dp[j]));
                   maxLen = Math.max(maxLen, dp[j]);
               }else{
                   dp[j] = 0;
               }
              prev = temp;
           }
       }

       return maxLen * maxLen;
    }
}
```