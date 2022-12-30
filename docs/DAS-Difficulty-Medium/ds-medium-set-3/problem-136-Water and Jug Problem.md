---
layout: default
title: Water and Jug Problem
parent: Medium Set 3
grand_parent: DSA Medium Difficulty
nav_order: 36
permalink: /problem-136-Water and Jug Problem/
---
# Water and Jug Problem
You are given two jugs with capacities jug1Capacity and jug2Capacity liters. There is an infinite amount of water supply available. Determine whether it is possible to measure exactly targetCapacity liters using these two jugs.

If targetCapacity liters of water are measurable, you must have targetCapacity liters of water contained within one or both buckets by the end.

Operations allowed:

* Fill any of the jugs with water.
* Empty any of the jugs.
* Pour water from one jug into another till the other jug is completely full, or the first jug itself is empty.

##### Example 1:
```markdown
Input: jug1Capacity = 3, jug2Capacity = 5, targetCapacity = 4
Output: true
Explanation: The famous Die Hard example
```
##### Example 2:
```markdown
Input: jug1Capacity = 2, jug2Capacity = 6, targetCapacity = 5
Output: false
```
##### Example 3:
```markdown
Input: jug1Capacity = 1, jug2Capacity = 2, targetCapacity = 3
Output: true
```
##### Constraints:
* 1 <= jug1Capacity, jug2Capacity, targetCapacity <= 10^6

### Solution:
every z = ax+by in range [0, x+y] is measurable.
```java
class Solution {
    public boolean canMeasureWater(int jug1Capacity, int jug2Capacity, int targetCapacity) {
        if(jug1Capacity + jug2Capacity < targetCapacity) return false;
        if(jug1Capacity == targetCapacity || jug2Capacity == targetCapacity || jug1Capacity + jug2Capacity == targetCapacity) return true;
        return targetCapacity % GCD(jug1Capacity, jug2Capacity) == 0;
    }

    public int GCD(int a, int b){
        if(b == 0) return a;
        return GCD(b, a % b);
    }
}
```