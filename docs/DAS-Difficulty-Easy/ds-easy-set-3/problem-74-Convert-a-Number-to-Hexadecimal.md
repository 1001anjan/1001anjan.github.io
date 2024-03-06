---
layout: default
title: Convert a Number to Hexadecimal
parent: Easy Set 3
grand_parent: DSA Easy
nav_order: 11
permalink: /problem-74-Convert-a-Number-to-Hexadecimal/
---
# Convert a Number to Hexadecimal

Given an integer num, return a string representing its hexadecimal representation. For negative integers, two’s complement method is used.

All the letters in the answer string should be lowercase characters, and there should not be any leading zeros in the answer except for the zero itself.

Note: You are not allowed to use any built-in library method to directly solve this problem.

##### Example 1:
```markdown
Input: num = 26
Output: "1a"
```
##### Example 2:
```markdown
Input: num = -1
Output: "ffffffff"
```
#### Constraints:
* -231 <= num <= 231 - 1

### Solution:
```java
class Solution {
    public String toHex(int num) {
        return Integer.toHexString(num);
    }
}
```

