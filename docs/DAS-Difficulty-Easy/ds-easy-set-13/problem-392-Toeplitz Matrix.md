---
layout: default
title: Toeplitz Matrix
parent: Easy Set 13
grand_parent: DSA Easy
nav_order: 22
permalink: /problem-392-Toeplitz Matrix/
---
# Toeplitz Matrix
Given an m x n matrix, return true if the matrix is Toeplitz. Otherwise, return false.

A matrix is Toeplitz if every diagonal from top-left to bottom-right has the same elements.

##### Example 1:
![](../../assets/images/ds/ex1test.jpeg)
```markdown
Input: matrix = [[1,2,3,4],[5,1,2,3],[9,5,1,2]]
Output: true
Explanation:
In the above grid, the diagonals are:
"[9]", "[5, 5]", "[1, 1, 1]", "[2, 2, 2]", "[3, 3]", "[4]".
In each diagonal all elements are the same, so the answer is True.
```
##### Example 2:
![](../../assets/images/ds/ex2test.jpeg)
```markdown
Input: matrix = [[1,2],[2,2]]
Output: false
Explanation:
The diagonal "[1, 2]" has different elements.
```
##### Constraints:
* m == matrix.length
* n == matrix[i].length
* 1 <= m, n <= 20
* 0 <= matrix[i][j] <= 99

##### Follow up:
* What if the matrix is stored on disk, and the memory is limited such that you can only load at most one row of the matrix into the memory at once?
* What if the matrix is so large that you can only load up a partial row into the memory at once?

### Solution:
```java
class Solution {
    public boolean isToeplitzMatrix(int[][] matrix) {
        for(int i = 0; i < matrix.length - 1; i++){
            for(int j = 0; j < matrix[i].length - 1; j++){
                if(matrix[i][j] != matrix[i + 1][j + 1]) return false;
            }
        }
        
        return true;
    }
}
```