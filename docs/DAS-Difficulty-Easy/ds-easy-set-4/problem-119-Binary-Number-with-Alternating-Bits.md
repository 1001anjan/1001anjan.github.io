---
layout: default
title: Binary Number with Alternating Bits
parent: Easy Set 4
grand_parent: DSA Easy Difficulty
nav_order: 19
permalink: /problem-119-Binary-Number-with-Alternating-Bits/
---
# Binary Number with Alternating Bits

Given a positive integer, check whether it has alternating bits: namely, if two adjacent bits will always have different values.

##### Example 1:
```markdown
Input: n = 5
Output: true
Explanation: The binary representation of 5 is: 101
```
##### Example 2:
```markdown
Input: n = 7
Output: false
Explanation: The binary representation of 7 is: 111.
```
##### Example 3:
```markdown
Input: n = 11
Output: false
Explanation: The binary representation of 11 is: 1011.
```
##### Constraints:
* 1 <= n <= 231 - 1

### Solution:
```java
class Solution {
    public boolean hasAlternatingBits(int n) {
       int curr = n%2;
        n = n/2;
        while(n>0){
            if(curr == n%2) return false;
            curr = n%2;
            n = n/2;
        }
        return true;
    }
}
```