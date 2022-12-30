---
layout: default
title: Check If It Is a Straight Line
parent: Easy Set 14
grand_parent: DSA Easy Difficulty
nav_order: 14
permalink: /problem-414-Check If It Is a Straight Line/
---
# Check If It Is a Straight Line
You are given an array coordinates, coordinates[i] = [x, y], where [x, y] represents the coordinate of a point. Check if these points make a straight line in the XY plane.

##### Example 1:
![](../../assets/images/ds/untitled-diagram-2.jpeg)
```markdown
Input: coordinates = [[1,2],[2,3],[3,4],[4,5],[5,6],[6,7]]
Output: true
```
##### Example 2:
![](../../assets/images/ds/untitled-diagram-11.jpeg)
```markdown
Input: coordinates = [[1,1],[2,2],[3,4],[4,5],[5,6],[7,7]]
Output: false
```
##### Constraints:
* 2 <= coordinates.length <= 1000
* coordinates[i].length == 2
* -10^4 <= coordinates[i][0], coordinates[i][1] <= 10^4
* coordinates contains no duplicate point.

### Solution:
The slope for a line through any 2 points (x0, y0) and (x1, y1) is (y1 - y0) / (x1 - x0); Therefore, for any given 3 points (denote the 3rd point as (x, y)), if they are in a straight line, the slopes of the lines from the 3rd point to the 2nd point and the 2nd point to the 1st point must be equal:

(y - y1) / (x - x1) = (y1 - y0) / (x1 - x0)
In order to avoid being divided by 0, use multiplication form:

(x1 - x0) * (y - y1) = (x - x1) * (y1 - y0) =>
dx * (y - y1) = dy * (x - x1), where dx = x1 - x0 and dy = y1 - y0

```java
class Solution {
    public boolean checkStraightLine(int[][] coordinates) {
        int dx = coordinates[1][0] - coordinates[0][0];
        int dy = coordinates[1][1] - coordinates[0][1];
        
        for(int i = 2; i < coordinates.length; i++){
            int dxi = coordinates[i][0] - coordinates[i - 1][0]; 
            int dyi = coordinates[i][1] - coordinates[i - 1][1];
            if(dx * dyi != dy * dxi) return false;
        }
        
        return true;
    }
}
```


