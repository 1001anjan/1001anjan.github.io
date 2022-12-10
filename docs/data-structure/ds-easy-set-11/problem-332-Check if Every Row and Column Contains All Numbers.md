---
layout: default
title: Check if Every Row and Column Contains All Numbers
parent: Data Structure Easy Set 11
grand_parent: Data Structure
nav_order: 22
permalink: /problem-332-Check if Every Row and Column Contains All Numbers/
---
# Check if Every Row and Column Contains All Numbers
An n x n matrix is valid if every row and every column contains all the integers from 1 to n (inclusive).

Given an n x n integer matrix matrix, return true if the matrix is valid. Otherwise, return false.

##### Example 1:
![](../../assets/images/ds/example1drawio.png)
```markdown
Input: matrix = [[1,2,3],[3,1,2],[2,3,1]]
Output: true
Explanation: In this case, n = 3, and every row and column contains the numbers 1, 2, and 3.
Hence, we return true.
```
##### Example 2:
![](../../assets/images/ds/example2drawio.png)
```markdown
Input: matrix = [[1,1,1],[1,2,3],[1,2,3]]
Output: false
Explanation: In this case, n = 3, but the first row and the first column do not contain the numbers 2 or 3.
Hence, we return false.
```
##### Constraints:
* n == matrix.length == matrix[i].length
* 1 <= n <= 100
* 1 <= matrix[i][j] <= n

### Solution:
```java
class Solution {
    public boolean checkValid(int[][] matrix) {
        //check for row
        int n = matrix.length;
        for(int i = 0;i < matrix.length; i++){
            Set<Integer> s = new HashSet<>();
            for(int j = 0; j < matrix[i].length; j++){
                s.add(matrix[i][j]);
            }
            if(s.size() != n){
                return false;
            }
        }
        
        //check for column
        for(int i = 0;i < matrix.length; i++){
            Set<Integer> s = new HashSet<>();
            for(int j = 0; j < matrix[i].length; j++){
                s.add(matrix[j][i]);
            }
            if(s.size() != n){
                return false;
            }
        }
        return true;
    }
}
```
##### Faster execution time
```java
class Solution {
    public boolean checkValid(int[][] matrix) {
        for(int i=0;i<matrix.length;i++){
            
            boolean [] checkrow = new boolean[matrix[i].length];
            for(int j= 0 ; j<checkrow.length;j++){
                int temp = matrix[i][j];
                if(checkrow[temp-1])
                    return false;
                checkrow[temp-1] = true;
            }
            
            boolean [] checkcol = new boolean[matrix[i].length];     
            for(int j= 0 ; j<checkcol.length;j++){
                int temp = matrix[j][i];
                if(checkcol[temp-1])
                    return false;
                checkcol[temp-1] = true;
            }
        }
        return true;
    }
}
```
