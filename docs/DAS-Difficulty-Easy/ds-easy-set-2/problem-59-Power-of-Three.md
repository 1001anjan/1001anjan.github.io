---
layout: default
title: Power of Three
parent: Easy Set 2
grand_parent: DSA Easy Difficulty
nav_order: 28
permalink: /problem-59-Power-of-Three/
---
# Power of Three

Given an integer n, return true if it is a power of three. Otherwise, return false.

An integer n is a power of three, if there exists an integer x such that n == 3x.

##### Example 1:
```markdown
Input: n = 27
Output: true
```
##### Example 2:
```markdown
Input: n = 0
Output: false
```
##### Example 3:
```markdown
Input: n = 9
Output: true
```
##### Constraints:
* -231 <= n <= 231 - 1

### Solution
```java
public class Solution {
    public boolean isPowerOfThree(int n) {
        if (n < 1) {
            return false;
        }

        while (n % 3 == 0) {
            n /= 3;
        }

        return n == 1;
    }
}
```