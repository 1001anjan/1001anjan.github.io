---
layout: default
title: Hamming Distance
parent: Easy Set 3
grand_parent: DSA Easy Difficulty
nav_order: 18
permalink: /problem-81-Hamming-Distance/
---
# Hamming Distance
The Hamming distance between two integers is the number of positions at which the corresponding bits are different.

Given two integers x and y, return the Hamming distance between them.

##### Example 1:
```markdown
Input: x = 1, y = 4
Output: 2
Explanation:
1   (0 0 0 1)
4   (0 1 0 0)
↑   ↑
The above arrows point to positions where the corresponding bits are different.
```
##### Example 2:
```markdown
Input: x = 3, y = 1
Output: 1
```
##### Constraints:
* 0 <= x, y <= 231 - 1

### Solution
```java
class Solution {
    public int hammingDistance(int x, int y) {
        int r = x ^ y;
        int c = 0;
        while(r>0){
            c = c + r%2;
            r = r/2;
        }
        return c;
    }
}
```