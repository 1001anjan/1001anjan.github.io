---
layout: default
title: Largest Triangle Area
parent: Data Structure Easy Set 13
grand_parent: Data Structure
nav_order: 28
permalink: /problem-398-Largest Triangle Area/
---
# Largest Triangle Area
Given an array of points on the X-Y plane points where points[i] = [xi, yi], return the area of the largest triangle that can be formed by any three different points. Answers within 10-5 of the actual answer will be accepted.

![](../../assets/images/ds/1027.png)
##### Example 1:
```markdown
Input: points = [[0,0],[0,1],[1,0],[0,2],[2,0]]
Output: 2.00000
Explanation: The five points are shown in the above figure. The red triangle is the largest.
```
##### Example 2:
```markdown
Input: points = [[1,0],[0,0],[0,1]]
Output: 0.50000
```
##### Constraints:
* 3 <= points.length <= 50
* -50 <= xi, yi <= 50
* All the given points are unique.

### Solution:
```java
class Solution {
    public double largestTriangleArea(int[][] points) {
        double max = 0.0;
        for(int i = 0; i < points.length - 2; i++){
            for(int j = i + 1; j < points.length - 1; j++){
                for(int k = j + 1; k < points.length; k++){
                    max = Math.max(max,calculateTriangleArea(points[i], points[j], points[k]));
                }
            }
        }
        return max;        
    }
    
    public double calculateTriangleArea(int[] p1, int[] p2, int[] p3){
        return Math.abs(p1[0]*(p2[1] - p3[1]) + p2[0]*(p3[1] - p1[1]) + p3[0]*(p1[1] - p2[1]))/2.0;
    }
}
```
