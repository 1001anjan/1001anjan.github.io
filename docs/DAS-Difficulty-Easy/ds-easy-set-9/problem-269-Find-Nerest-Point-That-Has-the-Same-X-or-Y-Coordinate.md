---
layout: default
title: Count Items Matching a Rule
parent: Easy Set 9
grand_parent: DSA Easy
nav_order: 19
permalink: /problem-269-Find-Nearest-Point-That-Has-the-Same-X-or-Y-Coordinate/
---
# Find Nearest Point That Has the Same X or Y Coordinate
You are given two integers, x and y, which represent your current location on a Cartesian grid: (x, y). You are also given an array points where each points[i] = [ai, bi] represents that a point exists at (ai, bi). A point is valid if it shares the same x-coordinate or the same y-coordinate as your location.

Return the index (0-indexed) of the valid point with the smallest Manhattan distance from your current location. If there are multiple, return the valid point with the smallest index. If there are no valid points, return -1.

The Manhattan distance between two points (x1, y1) and (x2, y2) is abs(x1 - x2) + abs(y1 - y2).

##### Example 1:
```markdown
Input: x = 3, y = 4, points = [[1,2],[3,1],[2,4],[2,3],[4,4]]
Output: 2
Explanation: Of all the points, only [3,1], [2,4] and [4,4] are valid. Of the valid points, [2,4] and [4,4] have the smallest Manhattan distance from your current location, with a distance of 1. [2,4] has the smallest index, so return 2.
```
##### Example 2:
```markdown
Input: x = 3, y = 4, points = [[3,4]]
Output: 0
Explanation: The answer is allowed to be on the same location as your current location.
```
##### Example 3:
```markdown
Input: x = 3, y = 4, points = [[2,3]]
Output: -1
Explanation: There are no valid points.
```
##### Constraints:
* 1 <= points.length <= 104
* points[i].length == 2
* 1 <= x, y, ai, bi <= 104

### Solution:
```java
class Solution {
    public int nearestValidPoint(int x, int y, int[][] points) {
        int md = Integer.MAX_VALUE;
        int index = -1;
        int i = 0;
        for(int[] p : points){
            if(p[0] == x || p[1] == y){
                int d = Math.abs(x - p[0]) + Math.abs(y - p[1]);
                if(md > d){
                    md = d;
                    index = i;
                }
            }
            i++;
        }
        return index;
    }
}
```
### Faster by nature
```java
class Solution {
    public int nearestValidPoint(int x, int y, int[][] points) {
        int md = Integer.MAX_VALUE;
        int index = -1;
        for(int i = 0; i < points.length; i++){
            if(points[i][0] == x || points[i][1] == y){
                int d = Math.abs(x - points[i][0]) + Math.abs(y - points[i][1]);
                if(md > d){
                    md = d;
                    index = i;
                }
            }
        }
        return index;
    }
}
```