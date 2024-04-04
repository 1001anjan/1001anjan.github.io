---
layout: default
title: Matrix Diagonal Sum
parent: Easy Set 8
grand_parent: DSA Easy
nav_order: 17
permalink: /problem-237-Matrix-Diagonal-Sum/
---
# Matrix Diagonal Sum
Given a square matrix mat, return the sum of the matrix diagonals.

Only include the sum of all the elements on the primary diagonal and all the elements on the secondary diagonal that are not part of the primary diagonal.

##### Example 1:
![](../../assets/images/ds/sample_1911.png)

```markdown
Input: mat = [[1,2,3],
[4,5,6],
[7,8,9]]
Output: 25
Explanation: Diagonals sum: 1 + 5 + 9 + 3 + 7 = 25
Notice that element mat[1][1] = 5 is counted only once.
```
##### Example 2:
```markdown
Input: mat = [[1,1,1,1],
[1,1,1,1],
[1,1,1,1],
[1,1,1,1]]
Output: 8
```
##### Example 3:
```markdown
Input: mat = [[5]]
Output: 5
```
##### Constraints:
* n == mat.length == mat[i].length
* 1 <= n <= 100
* 1 <= mat[i][j] <= 100

### Solution:
```java
class Solution {
    public int diagonalSum(int[][] mat) {
        int sum = 0;
        int i = 0;
        int j = 0;
        
        while(i < mat.length){
            sum += mat[i++][j++];
        }
        i = 0;
        j = mat[0].length - 1;
        
        while(i < mat.length){
            sum += mat[i++][j--];
        }
        if(mat.length % 2 != 0)
            sum -= mat[mat.length / 2][mat.length / 2];
        return sum;
    }
}
```