---
layout: default
title: Count Odd Numbers in an Interval Range
parent: Data Structure Easy Set 8
grand_parent: Data Structure
nav_order: 9
permalink: /problem-229-Count-Odd-Numbers-in-an-Interval-Range/
---
# Count Odd Numbers in an Interval Range

Given two non-negative integers low and high. Return the count of odd numbers between low and high (inclusive).

##### Example 1:
```markdown
Input: low = 3, high = 7
Output: 3
Explanation: The odd numbers between 3 and 7 are [3,5,7].
```
##### Example 2:
```markdown
Input: low = 8, high = 10
Output: 1
Explanation: The odd numbers between 8 and 10 are [9].
```
##### Constraints:
* 0 <= low <= high <= 10^9

### Solution:
```java
class Solution {
    public int countOdds(int low, int high) {
        int ans = (high - low)/2;
        if(low % 2 ==0 && high % 2 == 0 ) return ans;
        return ans + 1;
        
    }
}
```