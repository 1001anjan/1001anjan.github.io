---
layout: default
title: XOR Operation in an Array
parent: Easy Set 8
grand_parent: DSA Easy
nav_order: 3
permalink: /problem-223-XOR-Operation-in-an-Array/
---
# XOR Operation in an Array

You are given an integer n and an integer start.

Define an array nums where nums[i] = start + 2 * i (0-indexed) and n == nums.length.

Return the bitwise XOR of all elements of nums.

##### Example 1:
```markdown
Input: n = 5, start = 0
Output: 8
Explanation: Array nums is equal to [0, 2, 4, 6, 8] where (0 ^ 2 ^ 4 ^ 6 ^ 8) = 8.
Where "^" corresponds to bitwise XOR operator.
```
##### Example 2:
```markdown
Input: n = 4, start = 3
Output: 8
Explanation: Array nums is equal to [3, 5, 7, 9] where (3 ^ 5 ^ 7 ^ 9) = 8.
```
##### Constraints:
* 1 <= n <= 1000
* 0 <= start <= 1000
* n == nums.length

### Solution:
```java
class Solution {
    public int xorOperation(int n, int start) {
        int ans = start;
        for(int i = 1; i < n; i++)
            ans = ans ^ (start + 2*i);
        return ans;
    }
}
```