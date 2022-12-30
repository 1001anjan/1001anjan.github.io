---
layout: default
title: Range Addition IIRange Addition II
parent: Easy Set 13
grand_parent: DSA Easy Difficulty
nav_order: 14
permalink: /problem-384-Range Addition II/
---
# Range Addition II
You are given an m x n matrix M initialized with all 0's and an array of operations ops, where ops[i] = [ai, bi] means M[x][y] should be incremented by one for all 0 <= x < ai and 0 <= y < bi.

Count and return the number of maximum integers in the matrix after performing all the operations.

##### Example 1:

```markdown
Input: m = 3, n = 3, ops = [[2,2],[3,3]]
Output: 4
Explanation: The maximum integer in M is 2, and there are four of it in M. So return 4.
```
##### Example 2:
```markdown
Input: m = 3, n = 3, ops = [[2,2],[3,3],[3,3],[3,3],[2,2],[3,3],[3,3],[3,3],[2,2],[3,3],[3,3],[3,3]]
Output: 4
```
##### Example 3:
```markdown
Input: m = 3, n = 3, ops = []
Output: 9
```
##### Constraints:
* 1 <= m, n <= 4 * 104
* 0 <= ops.length <= 104
* ops[i].length == 2
* 1 <= ai <= m
* 1 <= bi <= n

### Solution: 
##### Memory limits exceeds 
```java
class Solution {
    // Goal should be to find that maxima grid which is common (overlapping) across ops[i] range. 
    // e.g: M[0][0] would always hold maxValue but it would not give us number of maximas
    // so if we keep on reducing row and columns by scanning ops set, we would end up with that maxima grid (r*c) :)

    // Runtime: 0 ms, faster than 100.00% of Java online submissions for Range Addition II.
    // Memory Usage: 42 MB, less than 99.81% of Java online submissions for Range Addition II.

    public int maxCount(int m, int n, int[][] ops) {
        int rowMinima = m; // number of row cells holding max value
        int colMinima = n; // number of column cells holding max value
        for(int i = 0; i < ops.length; i++){
            rowMinima = Math.min(rowMinima, ops[i][0]);
            colMinima = Math.min(colMinima, ops[i][1]);
        }
        return rowMinima * colMinima;
    }
}
```
##### Improvement 
