---
layout: default
title: Check if Matrix Is X-Matrix
parent: Easy Set 12
grand_parent: DSA Easy Difficulty
nav_order: 23
permalink: /problem-363-Check if Matrix Is X-Matrix/
---
# Check if Matrix Is X-Matrix
A square matrix is said to be an X-Matrix if both of the following conditions hold:

1. All the elements in the diagonals of the matrix are non-zero.
2. All other elements are 0.
Given a 2D integer array grid of size n x n representing a square matrix, return true if grid is an X-Matrix. Otherwise, return false.

##### Example 1:
![](../../assets/images/ds/ex11.jpeg)
```markdown
Input: grid = [[2,0,0,1],[0,3,1,0],[0,5,2,0],[4,0,0,2]]
Output: true
Explanation: Refer to the diagram above.
An X-Matrix should have the green elements (diagonals) be non-zero and the red elements be 0.
Thus, grid is an X-Matrix.
```
##### Example 2:
![](../../assets/images/ds/ex22.jpeg)
```markdown
Input: grid = [[5,7,0],[0,3,1],[0,5,0]]
Output: false
Explanation: Refer to the diagram above.
An X-Matrix should have the green elements (diagonals) be non-zero and the red elements be 0.
Thus, grid is not an X-Matrix.
```
##### Constraints:
* n == grid.length == grid[i].length
* 3 <= n <= 100
* 0 <= grid[i][j] <= 10^5

### Solution:
```java
class Solution {
    private boolean isDiagonal(int i, int j, int length) {
        return (i == j || j == length - 1 - i);
    }

    public boolean checkXMatrix(int[][] grid) {
        for(int i = 0; i < grid.length; i++) {
            for(int j = 0; j < grid[i].length; j++) {
                if(isDiagonal(i, j, grid.length)){
                    if(grid[i][j] == 0) return false;
                }else{
                    if(grid[i][j] != 0) return false;
                }                     
            }
        }
        return true;
    }
}
```