---
layout: default
title: Power of Four
parent: Data Structure Easy Set 2
grand_parent: Data Structure
nav_order: 30
permalink: /problem-61-a-Power-of-Four/
---
# Power of Four
Given an integer n, return true if it is a power of four. Otherwise, return false.

An integer n is a power of four, if there exists an integer x such that n == 4x.

##### Example 1:
```markdown
Input: n = 16
Output: true
```
##### Example 2:
```markdown
Input: n = 5
Output: false
```
##### Example 3:
```markdown
Input: n = 1
Output: true
```
##### Constraints:
* -231 <= n <= 231 - 1

### Solution
```java
class Solution {
    public boolean isPowerOfFour(int n) {
       if(n == 0) return false;
        while(n > 1){
           if(n%4 != 0) return false;
            n = n/4;
        }
        return n == 1;
    }
}
```