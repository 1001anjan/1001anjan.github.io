---
layout: default
title: Bitwise AND of Numbers Range
parent: Medium Set 2
grand_parent: DSA Medium Difficulty
nav_order: 45
permalink: /problem-95-Bitwise AND of Numbers Range/
---
# Bitwise AND of Numbers Range
Given two integers left and right that represent the range [left, right], return the bitwise AND of all numbers in this range, inclusive.

##### Example 1:
```markdown
Input: left = 5, right = 7
Output: 4
```
##### Example 2:
```markdown
Input: left = 0, right = 0
Output: 0
```
##### Example 3:
```markdown
Input: left = 1, right = 2147483647
Output: 0
```
##### Constraints:
* 0 <= left <= right <= 2^31 - 1

### Solution:
```java
class Solution {
    public int rangeBitwiseAnd(int left, int right) {
        while(left < right) right = right & (right - 1);
        return right;
    }
}
```