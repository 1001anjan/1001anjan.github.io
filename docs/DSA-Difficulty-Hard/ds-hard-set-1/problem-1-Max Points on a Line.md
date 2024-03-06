---
layout: default
title: Max Points on a Line
parent: Hard Set 1
grand_parent: DSA Hard
nav_order: 1
permalink: /problem-1-Max Points on a Line/
---

#  Max Points on a Line
Given an array of points where points[i] = [xi, yi] represents a point on the X-Y plane, return the maximum number of points that lie on the same straight line.

##### Example 1:
![](../../assets/images/ds/plane1.jpeg)
```markdown
Input: points = [[1,1],[2,2],[3,3]]
Output: 3
```
##### Example 2:
![](../../assets/images/ds/plane2.jpeg)
```markdown
Input: points = [[1,1],[3,2],[5,3],[4,1],[2,3],[1,4]]
Output: 4
```
##### Constraints:
* 1 <= points.length <= 300
* points[i].length == 2
* -10^4 <= xi, yi <= 10^4
* All the points are unique.

### Solution: 
![](../../assets/images/ds/149_max_points_on_a_line.drawio.png)
In this example, three interesting lines contain the point (4,1)(4, 1)(4,1) – the first line contains the points (4,1)(4, 1)(4,1) and (5,3)(5, 3)(5,3), the second one contains (4,1)(4, 1)(4,1), (3,2)(3, 2)(3,2), (2,3)(2, 3)(2,3) and (1,4)(1, 4)(1,4) and the third one contains (4,1)(4, 1)(4,1) and (1,1)(1, 1)(1,1). The angles between the X axis and the vectors from (4,1)(4, 1)(4,1) to the points (3,2)(3, 2)(3,2), (2,3)(2, 3)(2,3) and (1,4)(1, 4)(1,4) are equal (denoted with the green arc in the picture). In other words, all these vectors have the same atan2. On the other side, the vector from (4,1)(4, 1)(4,1) to (5,3)(5, 3)(5,3) has a different atan2 (denoted with the red arc). From this example, one can make the following observation:

We call a point outside if it belongs to a line, but it doesn't lie between any other two points on this line (it's one of the edges). The vectors from an outside point to all other points on the line have the same atan2. Now the problem reduces to the following:

For a fixed point points[i], consider all other points points[j] and calculate the atan2 for each vector points[j] - points[i] (the vector with the magnitudes (points[j].x - points[i].x, points[j].y - points[i].y)). Then find the maximum number of times some angle value occurs among the calculated values. One can use a hash map for this.

```java
class Solution {
    public int maxPoints(int[][] points) {
        int n = points.length;

        if(n == 1) return 1;
        int result = 2;

        for(int i = 0; i < n; i++){
            Map<Double, Integer> map = new HashMap<>();
            for(int j = 0; j < n; j++){
                if(i != j){
                    map.merge(Math.atan2(points[i][1] - points[j][1], points[i][0] - points[j][0]), 1, Integer::sum);
                }
            }
            result = Math.max(result, Collections.max(map.values()) + 1);
        }

        return result;
    }
}
```
##### Complexity Analysis
* Time complexity: O(n^2)
* Space complexity: O(n). We store O(n) values of atan2 in the hash map.