---
layout: default
title: Spiral Matrix
parent: Data Structure Medium Set 1
grand_parent: Data Structure
nav_order: 29
permalink: /problem-29-Spiral Matrix/
---
# Spiral Matrix
Given an m x n matrix, return all elements of the matrix in spiral order.

##### Example 1:
![](../../assets/images/ds/spiral1.jpeg)
```markdown
Input: matrix = [[1,2,3],[4,5,6],[7,8,9]]
Output: [1,2,3,6,9,8,7,4,5]
```
##### Example 2:
![](../../assets/images/ds/spiral.jpeg)
```markdown
Input: matrix = [[1,2,3,4],[5,6,7,8],[9,10,11,12]]
Output: [1,2,3,4,8,12,11,10,9,5,6,7]
```
##### Constraints:
* m == matrix.length
* n == matrix[i].length
* 1 <= m, n <= 10
* -100 <= matrix[i][j] <= 100

### Solution:
```java
class Solution {
    public List<Integer> spiralOrder(int[][] matrix) {
        List<Integer> ans = new ArrayList<>();
        int m = matrix.length;
        int n = matrix[0].length; 
        
        int total = m * n, count = 0;
        int i = 0, j = 0;
        int yRight = 0, yLeft = 0, xUp = 1, xDown = 0;
        while(count < total){
            while(count < total && j < n - yRight){
                ans.add(matrix[i][j]);
                j++;
                count++;
            }
            yRight++;
            i++;
            j--;
            while(count < total && i < m - xDown){
                ans.add(matrix[i][j]);
                count++;
                i++;
            }
            xDown++;
            i--;
            j--;
            while(count < total && j >= yLeft){
                ans.add(matrix[i][j]);
                count++;
                j--;
            }
            yLeft++;
            j++;
            i--;
            while(count < total && i >= xUp){
                ans.add(matrix[i][j]);
                i--;
                count++;
            }
            i++;
            j++;
            xUp++;
        }

        return ans;
    }
}
```
