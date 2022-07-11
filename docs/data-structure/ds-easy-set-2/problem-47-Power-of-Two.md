---
layout: default
title: Power of Two
parent: Data Structure Easy Set 2
grand_parent: Data Structure
nav_order: 16
permalink: /problem-47-Power-of-Two/
---
# Power of Two
Given an integer n, return true if it is a power of two. Otherwise, return false.

An integer n is a power of two, if there exists an integer x such that n == 2x.

##### Example 1:
```markdown
Input: n = 1
Output: true
Explanation: 20 = 1
```
##### Example 2:
```markdown
Input: n = 16
Output: true
Explanation: 24 = 16
```
##### Example 3:
```markdown
Input: n = 3
Output: false
```
##### Constraints:
* -231 <= n <= 231 - 1

### Solution
```java
class Solution {
    public boolean isPowerOfTwo(int n) {
        if(n == 1) return true;
        if(n == 0) return false;
        while(n>=0){
            if(n == 0) return true;
            if(n == 2) return true;
            if(n % 2 == 1) return false;
            n = n/2;
        }
        return false;
    }
}
```