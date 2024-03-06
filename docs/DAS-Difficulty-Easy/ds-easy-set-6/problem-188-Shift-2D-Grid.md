---
layout: default
title: Shift 2D Grid
parent: Easy Set 6
grand_parent: DSA Easy
nav_order: 28
permalink: /problem-188-Shift-2D-Grid/
---
# Shift 2D Grid
Given a 2D grid of size m x n and an integer k. You need to shift the grid k times.

In one shift operation:

* Element at grid[i][j] moves to grid[i][j + 1].
* Element at grid[i][n - 1] moves to grid[i + 1][0].
* Element at grid[m - 1][n - 1] moves to grid[0][0].
* Return the 2D grid after applying shift operation k times.

##### Example 1:
![](../../assets/images/ds/e1.png![img.png](img.png))
```markdown
Input: grid = [[1,2,3],[4,5,6],[7,8,9]], k = 1
Output: [[9,1,2],[3,4,5],[6,7,8]]
```
##### Example 2:
![](../../assets/images/ds/e2.png)
```markdown
Input: grid = [[3,8,1,9],[19,7,2,5],[4,6,11,10],[12,0,21,13]], k = 4
Output: [[12,0,21,13],[3,8,1,9],[19,7,2,5],[4,6,11,10]]
```
##### Example 3:
```markdown
Input: grid = [[1,2,3],[4,5,6],[7,8,9]], k = 9
Output: [[1,2,3],[4,5,6],[7,8,9]]
```
##### Constraints:
* m == grid.length
* n == grid[i].length
* 1 <= m <= 50
* 1 <= n <= 50
* -1000 <= grid[i][j] <= 1000
* 0 <= k <= 100

### Solution:
```java
class Solution {
      public List<List<Integer>> shiftGrid(int[][] grid, int k) {
          
        int[][] ans = new int[grid.length][grid[0].length];

        for (int i = 0; i < grid.length; i++) {
            
            for (int j = 0; j < grid[0].length; j++) {

                int newCol = (j + k) % grid[0].length;

                int newRow = (i + (j + k) / grid[0].length) % grid.length;

                ans[newRow][newCol] = grid[i][j];

            }
        }

        return (List) Arrays.asList(ans);
    }
}
```