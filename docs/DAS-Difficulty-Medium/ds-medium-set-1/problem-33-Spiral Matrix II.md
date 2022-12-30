---
layout: default
title: Spiral Matrix II
parent: Medium Set 1
grand_parent: DSA Medium Difficulty
nav_order: 33
permalink: /problem-33-Spiral Matrix II/
---
# Spiral Matrix II
Given a positive integer n, generate an n x n matrix filled with elements from 1 to n2 in spiral order.

##### Example 1:
![](../../assets/images/ds/spiraln.jpeg)
```markdown
Input: n = 3
Output: [[1,2,3],[8,9,4],[7,6,5]]
```
##### Example 2:
```markdown
Input: n = 1
Output: [[1]]
```
##### Constraints:
* 1 <= n <= 20

### Solution: 
```java
class Solution {
    public int[][] generateMatrix(int n) {
        int[][] mat = new int[n][n];
        int c = 1, total = n * n;

        int i = 0, j = 0, yRight = 0, yLeft = 0, xUp = 1, xDown = 0;

        while(c <= total){
            while(c <= total && j < n - yRight) mat[i][j ++] = c ++;
            yRight ++;
            j--;
            i++;

            while(c <= total && i < n - xDown) mat[i ++][j] = c ++;
            xDown ++;
            i --;
            j --;

            while(c <= total && j >= yLeft) mat[i][j --] = c ++;
            yLeft++;
            j++;
            i --;

            while(c <= total && i >= xUp) mat[i --][j] = c ++;
            xUp++;
            i++;
            j++;

        }

        return mat;
    }
}
```