---
layout: default
title: Search a 2D Matrix II
parent: Data Structure Medium Set 3
grand_parent: Data Structure
nav_order: 8
permalink: /problem-108-Search a 2D Matrix II/
---
# Search a 2D Matrix II
Write an efficient algorithm that searches for a value target in an m x n integer matrix matrix. This matrix has the following properties:

* Integers in each row are sorted in ascending from left to right.
* Integers in each column are sorted in ascending from top to bottom.

##### Example 1:
![](../../assets/images/ds/searchgrid2.jpeg)
```markdown
Input: matrix = [[1,4,7,11,15],[2,5,8,12,19],[3,6,9,16,22],[10,13,14,17,24],[18,21,23,26,30]], target = 5
Output: true
```
##### Example 2:
![](../../assets/images/ds/searchgrid.jpeg)
```markdown
Input: matrix = [[1,4,7,11,15],[2,5,8,12,19],[3,6,9,16,22],[10,13,14,17,24],[18,21,23,26,30]], target = 20
Output: false
```
##### Constraints:
* m == matrix.length
* n == matrix[i].length
* 1 <= n, m <= 300
* -10^9 <= matrix[i][j] <= 10^9
* All the integers in each row are sorted in ascending order.
* All the integers in each column are sorted in ascending order.
* -10^9 <= target <= 10^9

### Solution:
```java
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        int row = 0;
        int col = matrix[0].length - 1;

        while(col >= 0 && row < matrix.length){
            if(matrix[row][col] == target) return true;
            if(matrix[row][col] > target){
                if(col >= 0) col --;
                else row ++;
            }else{
                if(row < matrix.length){
                    row ++;
                }else{
                    col --;
                }
            }
        }

        return false;
    }
}
```