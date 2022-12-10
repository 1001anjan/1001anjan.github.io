---
layout: default
title: Valid Boomerang
parent: Data Structure Easy Set 6
grand_parent: Data Structure
nav_order: 7
permalink: /problem-167-Valid-Boomerang/
---
# Valid Boomerang

Given an array points where points[i] = [xi, yi] represents a point on the X-Y plane, return true if these points are a boomerang.

A boomerang is a set of three points that are all distinct and not in a straight line.

##### Example 1:
```markdown
Input: points = [[1,1],[2,3],[3,2]]
Output: true
```
##### Example 2:
```markdown
Input: points = [[1,1],[2,2],[3,3]]
Output: false
```
##### Constraints:
* points.length == 3
* points[i].length == 2
* 0 <= xi, yi <= 100

### Solution: Area of a triangle 
```java
class Solution {
    public boolean isBoomerang(int[][] points) {
        double a, b, c, d, area;
        a=points[0][0]-points[1][0];
        b=points[1][0]-points[2][0];
        c=points[0][1]-points[1][1];
        d=points[1][1]-points[2][1];
        area=0.5*((a*d)-(b*c));
        return area!=0;
    }
}
```