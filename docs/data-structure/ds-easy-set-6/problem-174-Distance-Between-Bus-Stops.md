---
layout: default
title: Distance Between Bus Stops
parent: Data Structure Easy Set 6
grand_parent: Data Structure
nav_order: 14
permalink: /problem-174-Distance-Between-Bus-Stops/
---
# Distance Between Bus Stops
A bus has n stops numbered from 0 to n - 1 that form a circle. We know the distance between all pairs of neighboring stops where distance[i] is the distance between the stops number i and (i + 1) % n.

The bus goes along both directions i.e. clockwise and counterclockwise.

Return the shortest distance between the given start and destination stops.

##### Example 1:
![](../../assets/images/ds/untitled-diagram-1.jpeg)
```markdown
Input: distance = [1,2,3,4], start = 0, destination = 1
Output: 1
Explanation: Distance between 0 and 1 is 1 or 9, minimum is 1.
```
##### Example 2:
![](../../assets/images/ds/untitled-diagram-1-1.jpeg)
```markdown
Input: distance = [1,2,3,4], start = 0, destination = 2
Output: 3
Explanation: Distance between 0 and 2 is 3 or 7, minimum is 3.
```
##### Example 3:
![](../../assets/images/ds/untitled-diagram-1-2.jpeg)
```markdown
Input: distance = [1,2,3,4], start = 0, destination = 3
Output: 4
Explanation: Distance between 0 and 3 is 6 or 4, minimum is 4.
```
##### Constraints:
* 1 <= n <= 10^4
* distance.length == n
* 0 <= start, destination < n
* 0 <= distance[i] <= 10^4

### Solution:
```java
class Solution {
    public int distanceBetweenBusStops(int[] distance, int start, int destination) {
        int dist = 0;
        int sum = 0;
        if(start > destination){
            int t = destination;
            destination = start;
            start = t;
        }
        for(int i = 0; i<distance.length; i++){
            sum += distance[i];
            if(i >= start && i < destination)
                dist += distance[i];
        }
        System.out.println(dist);
        return Math.min(dist,sum-dist);
    }
}
```