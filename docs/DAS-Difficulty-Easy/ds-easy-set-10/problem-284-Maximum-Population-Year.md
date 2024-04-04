---
layout: default
title: Maximum-Population-Year
parent: Easy Set 10
grand_parent: DSA Easy
nav_order: 4
permalink: /problem-284-Maximum-Population-Year/
---
# Maximum Population Year
You are given a 2D integer array logs where each logs[i] = [birthi, deathi] indicates the birth and death years of the ith person.

The population of some year x is the number of people alive during that year. The ith person is counted in year x's population if x is in the inclusive range [birthi, deathi - 1]. Note that the person is not counted in the year that they die.

Return the earliest year with the maximum population.

##### Example 1:
```markdown
Input: logs = [[1993,1999],[2000,2010]]
Output: 1993
Explanation: The maximum population is 1, and 1993 is the earliest year with this population.
```
##### Example 2:
```markdown
Input: logs = [[1950,1961],[1960,1971],[1970,1981]]
Output: 1960
Explanation:
The maximum population is 2, and it had happened in years 1960 and 1970.
The earlier year between them is 1960.
```
##### Constraints:
* 1 <= logs.length <= 100
* 1950 <= birthi < deathi <= 2050

### Solution
```java
class Solution {
    public int maximumPopulation(int[][] logs) {
        int[] years = new int[101];
        
        for(int[] p : logs){
            years[p[0] - 1950]++;
            years[p[1] - 1950]--;
        }
        
        int max = Integer.MIN_VALUE;
        int y = 0;
        int curr = 0;
        for(int i = 0; i < 101; i++) {
            curr += years[i];
            if(curr > max) {
                max = curr;
                y = i + 1950;
            }
        }
        
        return y;
        
    }
}
```