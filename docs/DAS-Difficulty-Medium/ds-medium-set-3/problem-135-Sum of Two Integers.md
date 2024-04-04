---
layout: default
title: Sum of Two Integers
parent: Medium Set 3
grand_parent: DSA Medium
nav_order: 35
permalink: /problem-135-Sum of Two Integers/
---
# Sum of Two Integers
Given two integers a and b, return the sum of the two integers without using the operators + and -.

##### Example 1:
```markdown
Input: a = 1, b = 2
Output: 3
```
##### Example 2:
```markdown
Input: a = 2, b = 3
Output: 5
```
##### Constraints:
* -1000 <= a, b <= 1000

### Solution:
```java
class Solution {
    public int getSum(int a, int b) {
        if(b == 0) return a;
        int carry = (a & b) << 1;
        int sum = a ^ b;
        return getSum(sum, carry);
    }
}
```