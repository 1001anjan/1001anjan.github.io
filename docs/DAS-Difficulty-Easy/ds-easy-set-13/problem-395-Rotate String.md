---
layout: default
title: Rotate String
parent: Easy Set 13
grand_parent: DSA Easy
nav_order: 25
permalink: /problem-395-Rotate String/
---
# Rotate String
Given two strings s and goal, return true if and only if s can become goal after some number of shifts on s.

A shift on s consists of moving the leftmost character of s to the rightmost position.

For example, if s = "abcde", then it will be "bcdea" after one shift.

##### Example 1:
```markdown
Input: s = "abcde", goal = "cdeab"
Output: true
```
##### Example 2:
```markdown
Input: s = "abcde", goal = "abced"
Output: false
```
##### Constraints:
* 1 <= s.length, goal.length <= 100
* s and goal consist of lowercase English letters.

### Solution:
```java
class Solution {
    public boolean rotateString(String s, String goal) {
        if(goal.length() < s.length()) return false;
        return (goal + goal).indexOf(s) != -1;
    }
}
```